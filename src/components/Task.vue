<template>
    <div @click="$emit('toggle-reminder', task.id)" :class="['task px-2',task.reminder? 'border-l-4 green' : '']">
        <div class="flex justify-between items-center">{{task.text}}
            <i @click="onDeletedTask(task.id)" class="fa fa-window-close text-red-600"></i>
        </div>
        <div class="text-gray-500">{{task.day}}</div>
    </div>
    
</template>

<script>
export default {
    name: 'Task',
    props: ['task'],

    methods: {
        onDeletedTask(id) {
            this.$emit('delete-task', id)
        }
    }
}
</script>

<style>
    .green {
        border-left-color: green;
    }
</style>