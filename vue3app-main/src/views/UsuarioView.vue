<template>
    <div class="usuario">
        <h1>Usuários</h1>
         <!-- Campos de entrada para o cadastro de usuários -->
        <p><label for="nome">Nome: </label><input id="nome" type="text" v-model="usuario.nome"/></p>
        <p><label for="senha">Senha: </label><input id="senha" type="text" v-model="usuario.senha"/></p>
        <p><label for="demissao">Situação: </label><input id="demissao" type="date" v-model="usuario.demissao"/></p>
        <button @click="incluir">Incluir</button>

        <div v-if="usuarios.length === 0 && erro">
          <p>{{ erro }}</p>
        </div>
        <table v-else>
          <thead>
            <td>Id</td>
            <td>Nome</td>
            <td>Senha</td>
            <td>Situação</td>
          </thead>
          <tbody>
            <tr v-for="usuario in usuarios" :key="usuario.id">
              <td>{{ usuario.id }}</td>
              <td>{{ usuario.nome }}</td>
              <td>{{ usuario.senha }}</td>
              <td>{{ situacao(usuario.demissao) }}</td>
            </tr>
          </tbody>
        </table>
    </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue';
import axios from 'axios';
  
  const usuario = ref(
    {
      nome: '',
      senha: '',
      demissao: '',
    });

  const usuarios = ref([]);
  const erro = ref("");

  async function incluir() {
    erro.value = "";
    try{
      await axios.post("usuario", usuario.value);
      limparCampos(); // Limpar os campos após o cadastro
      await buscarTodosUsuarios(); // Atualizar a lista
    }
    catch(e) {
      erro.value = (e as Error).message;
    }
  }

// Função para limpar os campos do formulário
function limparCampos() {
  usuario.value = {
    id: '',
    nome: '',
    senha: '',
    demissao: '',
  };
}

  async function buscarTodosUsuarios() {
  try {
    const response = await axios.get('usuario');
    usuarios.value = response.data;
  } catch (e) {
    erro.value = (e as Error).message;
  }
}

  async function buscarUsuarios() {
    usuarios.value = (await axios.get("usuario")).data;
  }

// Função para determinar a situação de um usuário
function situacao(demissao: Date | null) {
  return demissao ? 'Demitido em ' : 'Ativo';
}

  onMounted(() => {
    buscarUsuarios();
  });

</script>