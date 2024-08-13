<script setup>
import { reactive } from 'vue';

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
  const getNumeroDeTarefasPendentes = () => {
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
        return getNumeroDeTarefasPendentes();
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

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getNumeroDeTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">

        <div class="col">
          <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required class="form-control" type="text" placeholder="Digite aqui a tarefa" name="" id="">
        </div>

        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>

        <div class="col-md-2">
          <select @change ="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>

      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done:tarefa.finalizada === true}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo}}
        </label>
      </li>
    </ul>
  </div>


</template>

<style scoped>

.done {
  text-decoration: line-through;
}
</style>
