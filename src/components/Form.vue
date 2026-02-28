<script setup>
    const props = defineProps(['registerTask', 'tempTask', 'filter', 'taskEdit', 'filterEdit'])
</script>

<template>
    <form @submit.prevent="props.registerTask">
        <div class="row">
            <div class="col">
                <input :value="props.tempTask" @change="props.taskEdit"
                    type="text" class="form-control" placeholder="Type your task:" required />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-success">Send</button>
            </div>
            <div class="d-flex col-md-2 align-items-center flex-column">
                <select class="form-control d-block" @change="props.filterEdit">
                    <option value="all">All tasks</option>
                    <option value="pending">Pending tasks</option>
                    <option value="completed">Completed tasks</option>
                </select>
                <h6 class="m-1 d-block">{{ props.filter }}</h6>
            </div>
        </div>
    </form>
</template>
