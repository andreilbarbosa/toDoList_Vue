<script setup>
const props = defineProps(['filtredTask'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.filtredTask">
            <input type="checkbox" @change="(evento) => (tarefa.finalizada = evento.target.checked)"
                :checked="tarefa.finalizada" :id="tarefa.titulo" />
            <label class="ms-3" :class="{ done: tarefa.finalizada }" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>