<h3 align="center">ITE002 – 2023</h3> 

Utilize os projetos contidos nos repositórios https://github.com/mineda/springboot3app e https://github.com/mineda/vue3app para:

1) Altere o nome do arquivo "AboutView.vue" para "UsuarioView.vue" para que fique coerente com o conteúdo. Também altere o texto do link de "About" para "Usuários". Faça as
modificações necessárias para que o sistema funcione com o arquivo alterado;

2) Inclua uma nova coluna para guardar a data de demissão (apenas a data, sem hora) na tabela "usr_usuario". A coluna deve aceitar valores nulos. Faça o mapeamento da coluna na classe
correspondente;

3) Na tela de cadastro de usuários, apresente uma nova coluna chamada “situação”. Seu valor deve ser “Ativo” se a data de demissão for nula, ou “Demitido em XX/XX/XXXX” (substituir XX/XX/XXXX pela data de demissão), caso contrário;

4) Crie uma função de demissão que preencha a data de demissão de um usuário.

Dicas:

• Em caso de erro por diferença de versões do Java, use o comando "mvn clean" no terminal;
• Para entradas do tipo "date" é possíve utilizar o tipo "date" de "input" (https://www.w3schools.com/tags/att_input_type_date.asp).
