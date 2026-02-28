<script setup>
    const props = defineProps(['pendingTasks']);
</script>

<template>
    <header class="p-5 m-4 mt-4 bg-light rounded-3">
        <h1>Today's Taks</h1>
        <p>You have {{ props.pendingTasks }} pending tasks</p>
    </header>
</template>
