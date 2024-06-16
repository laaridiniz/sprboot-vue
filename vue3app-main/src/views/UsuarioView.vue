<template>
    <div class="usuario">
        <h1>Usuários</h1>
        <p><label for="nome">Nome: </label><input id="nome" type="text" v-model="usuario.nome"/></p>
        <p><label for="senha">Senha: </label><input id="senha" type="text" v-model="usuario.senha"/></p>
        <p><label for="demissao">Situação: </label><input id="demissao" type="date" v-model="usuario.demissao"/></p>
        <p>{{ erro }}</p>
        <table>
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
              <td>{{ usuario.demissao }}</td>
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
      demissao: Date,
    });

  const usuarios = ref();
  const erro = ref("");

  async function incluir() {
    erro.value = "";
    try{
      await axios.post("usuario", usuario.value);
    }
    catch(e) {
      erro.value = (e as Error).message;
    }
    buscarUsuarios();
  }

  async function buscarUsuarios() {
    usuarios.value = (await axios.get("usuario")).data;
  }

  onMounted(() => {
    buscarUsuarios();
  });

</script>