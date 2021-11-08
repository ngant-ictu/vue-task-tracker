<template>
    <div>
        <ul>
            <li v-for="task in tasks" :key="task.id" class="border-b border-solid pb-2 mb-4 last:border-0">
                <Task @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task" />
            </li>
        </ul>
    </div>
</template>

<script>
import Task from '@/components/Task'
export default { 
    name: 'Tasks',
    components: {
        Task
    },
    props: ['tasks'],

    methods: {
        
    }
}
</script>

<style>
    
</style>