<template>
  <div>
    <h2>Cadastro de Jogadores</h2>

    <form @submit.prevent="adicionarJogador">
      <label for="nome">Nome:</label>
      <input
        v-model="nome"
        id="nome"
        type="text"
        placeholder="Nome do jogador"
      />

      <label for="idade">Idade:</label>
      <input v-model="idade" id="idade" type="number" placeholder="Idade" />

      <label for="corCamisa">Cor da Camisa:</label>
      <input
        v-model="corCamisa"
        id="corCamisa"
        type="text"
        placeholder="Cor da camisa"
      />

      <button type="submit">Cadastrar</button>
    </form>

    <div v-if="jogadores.length === 0">
      <p>Nenhum jogador cadastrado. Adicione um novo jogador.</p>
    </div>
    <ul v-else>
      <li v-for="(jogador, index) in jogadores" :key="index">
        {{ jogador.nome }} ({{ jogador.idade }} anos) - Camisa:
        {{ jogador.corCamisa }}
        <button @click="removerJogador(index)">Remover</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from "vue";

const nome = ref("");
const idade = ref("");
const corCamisa = ref("");
const jogadores = ref([]);

function adicionarJogador() {
  if (nome.value && idade.value && corCamisa.value) {
    jogadores.value.push({
      nome: nome.value,
      idade: idade.value,
      corCamisa: corCamisa.value,
    });
    nome.value = "";
    idade.value = "";
    corCamisa.value = "";
  } else {
    alert("Preencha todos os campos.");
  }
}

function removerJogador(index) {
  jogadores.value.splice(index, 1);
}
</script>

<style scoped>
form {
  margin-bottom: 20px;
}

input {
  margin: 5px;
}

button {
  margin: 5px;
}
</style>
