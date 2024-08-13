<script setup>
import { reactive } from 'vue';
import Tarefas from './components/Tarefas.vue'
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';

// array de objetos - criação de estado para as tarefas
const estado = reactive({
  tarefaTemporaria: '',
  filtro: 'todas',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Ir para a academia',
      finalizada: true,
    }
  ]
})

//função para retornar o numero de tarefas pendentes
const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

//retorna numero de tarefas finalizadas
const getNumeroDeTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

//função para retornar as tarefas a partir de uma filtragem
const getTarefasFiltradas = () => {
  const { filtro } = estado; //acessando filtro dentro do estado

  // aqui fazemos varios IFS, onde finalizada seja === true
  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getNumeroDeTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemporaria = '';
}

const editaTarefaTemporaria = (evento) => {
  estado.tarefaTemporaria = evento.target.value;
};
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario 
      :trocar-filtro="evento => estado.filtro = evento.target.value"
      :tarefa-temporaria="estado.tarefaTemporaria" 
      :cadastra-tarefa="cadastraTarefa"
      :edita-tarefa-temporaria="editaTarefaTemporaria" />
    <Tarefas :tarefas="getTarefasFiltradas()" />
  </div>


</template>
