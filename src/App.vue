<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: '',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Study TypeScript',
        finalizada: false,
      },
      {
        titulo: 'Study Vue.js',
        finalizada: true,
      },
      {
        titulo: 'Study Javascript',
        finalizada: false,
      }
    ]
  })

  function completeTask(evento){
    if(evento){
      return true;
    }else{
      return false;
    }
  }

  const getPendingTasks = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getCompletedTasks = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getFiltredTasks = () =>{
    const { filtro } = estado;

    switch (filtro){
      case 'pending':
        return getPendingTasks();
      case 'completed':
        return getCompletedTasks();
      default:
        return estado.tarefas;
    }
  }

  const taskRegister = () =>{
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }

    estado.tarefas.push(tarefaNova);

    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 m-4 mt-4 bg-light rounded-3">
      <h1>Today's Taks</h1>
      <p>
        You have {{ getPendingTasks().length}} pending tasks
      </p>
    </header>
    <form @submit.prevent="taskRegister">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" type="text" class="form-control" placeholder="Type your task:">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-success">Send</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="evento => estado.filtro = evento.target.value">
            <option value="all">All tasks</option>
            <option value="pending">Pending tasks</option>
            <option value="completed">Completed tasks</option>
          </select>
          {{ estado.filtro }}
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getFiltredTasks()">
        <input type="checkbox" @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" />
        <label class="ms-3" :class="{ done: completeTask(tarefa.finalizada)}"  :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done{
    text-decoration: line-through;
  }
</style>
