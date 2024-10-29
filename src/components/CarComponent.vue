<template>
  <div class="car-component">
    <h2>Garagem Digital - Cadastro de Carros</h2>

    <!-- Mensagem de Feedback -->
    <div v-if="message" class="message">{{ message }}</div>

    <!-- Formulário de Cadastro -->
    <div class="form">
      <input v-model="marca" placeholder="Marca do Carro" />
      <input v-model="modelo" placeholder="Modelo do Carro" />
      <input v-model="ano" placeholder="Ano de Fabricação" type="number" />
      <button @click="cadastrarCarro">Cadastrar Carro</button>
    </div>

    <!-- Lista de Carros Cadastrados -->
    <ul v-if="carros.length > 0" class="cars-list">
      <li v-for="(carro, index) in carros" :key="index">
        <strong>{{ carro.marca }}</strong> - {{ carro.modelo }} - {{ carro.ano }}
        <button @click="deletarCarro(index)">Deletar</button>
      </li>
    </ul>

    <!-- Mensagem de Lista Vazia -->
    <p v-else>Não há carros cadastrados ainda.</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const marca = ref('');
const modelo = ref('');
const ano = ref('');
const carros = ref([]);
const message = ref('');

const cadastrarCarro = () => {
  if (marca.value && modelo.value && ano.value) {
    const novoCarro = {
      marca: marca.value,
      modelo: modelo.value,
      ano: ano.value
    };
    carros.value.push(novoCarro);
    marca.value = '';
    modelo.value = '';
    ano.value = '';
    message.value = 'Carro cadastrado com sucesso!';
    setTimeout(() => { message.value = ''; }, 3000);
  } else {
    message.value = 'Preencha todos os campos antes de cadastrar.';
    setTimeout(() => { message.value = ''; }, 3000);
  }
};

const deletarCarro = (index) => {
  carros.value.splice(index, 1);
  message.value = 'Carro deletado com sucesso!';
  setTimeout(() => { message.value = ''; }, 3000);
};
</script>

<style scoped>
.car-component {
  padding: 20px;
  max-width: 500px;
  margin: 0 auto;
  text-align: center;
}

.form input {
  margin: 5px;
  padding: 10px;
  width: 80%;
}

.form button {
  margin: 10px;
  padding: 10px 20px;
  cursor: pointer;
}

.message {
  color: green;
  margin: 10px 0;
}

.cars-list {
  list-style-type: none;
  padding: 0;
}

.cars-list li {
  margin: 10px 0;
  background-color: #f0f0f0;
  padding: 10px;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

button {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  border-radius: 3px;
}
</style>
