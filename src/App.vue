<script setup>
import { reactive } from 'vue';
import Formulario from './components/Formulario.vue';
import Resultado from './components/Resultado.vue';

// Criação de estado para o cálculo com valores iniciais
const estado = reactive({
  numero1: 0,
  numero2: 0,
  operacao: 'soma',
  resultado: 0
});

// Função para calcular o resultado dependendo do cálculo escolhido
const calcula = () => {
  switch (estado.operacao) {
    case 'soma':
      estado.resultado = estado.numero1 + estado.numero2;
      break;
    case 'subtracao':
      estado.resultado = estado.numero1 - estado.numero2;
      break;
    default:
      estado.resultado = 0;
  }
};

// Funções para atualizar os valores e chamar o cálculo
const atualizaNumero1 = (evento) => {
  estado.numero1 = Number(evento.target.value);
  calcula();
};

const atualizaNumero2 = (evento) => {
  estado.numero2 = Number(evento.target.value);
  calcula();
};

const atualizaOperacao = (evento) => {
  estado.operacao = evento.target.value;
  calcula();
};
</script>

<template>
  <div class="container">
    <Formulario 
      :numero1="estado.numero1"
      :numero2="estado.numero2"
      :operacao="estado.operacao"
      :atualizaNumero1="atualizaNumero1"
      :atualizaNumero2="atualizaNumero2"
      :atualizaOperacao="atualizaOperacao"
    />
    <Resultado :resultado="estado.resultado" />
  </div>
</template>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  color: white;
  font-weight: bold;
  font-size: 40px;
  align-items: center;
  background-color: rgb(43, 43, 43);
  padding-top: 200px;
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.container input {
  display: block;
  padding: 5px;
  margin-bottom: 20px;
}

.container select {
  margin: 0 auto;
  display: block;
  margin-bottom: 20px;
}

</style>
