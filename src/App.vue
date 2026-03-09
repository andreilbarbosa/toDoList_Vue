<script setup>
import { reactive } from "vue";
import Head from "./components/Head.vue";
import Form from './components/Form.vue';
import ToDoList from "./components/ToDoList.vue";

const estado = reactive({
  filtro: "",
  tarefaTemp: "",
  tarefas: [
    {
      titulo: "Like in my project :D!",
      finalizada: false,
    },
  ],
});

function completeTask(evento) {
  if (evento) {
    return true;
  } else {
    return false;
  }
}

const getPendingTasks = () => {
  return estado.tarefas.filter((tarefa) => !tarefa.finalizada);
};

const getCompletedTasks = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada);
};

const getFiltredTasks = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pending":
      return getPendingTasks();
    case "completed":
      return getCompletedTasks();
    default:
      return estado.tarefas;
  }
};

const registerTask = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };

  estado.tarefas.push(tarefaNova);

  estado.tarefaTemp = "";
};
</script>

<!-- // -->

<template>
  <div class="container">
    <Head :pending-tasks="getPendingTasks().length" />
    <Form  :register-task="registerTask" :filter-edit="evento => estado.filtro = evento.target.value" :filter="estado.filtro" :temp-task="estado.tarefaTemp" :task-edit="evento => estado.tarefaTemp = evento.target.value" />
    <ToDoList :filtred-task="getFiltredTasks()" />
  </div>
</template>
