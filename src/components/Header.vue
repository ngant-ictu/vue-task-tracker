<template>
    <header class="flex justify-between items-center mb-4 py-5">
        <h1 class="text-3xl font-bold">{{ title }}</h1>
        <Button v-show="homePage" @toggle-add-task="$emit('toggle-add-task')" :text="showAddTask? 'Close' : 'Add Task'" :color=" showAddTask? 'red' : 'green'" />
    </header>
</template>

<script>
import Button from '@/components/Button'

export default {
    name: 'Header',
    components: {
        Button
    },
    props: {
        title: String,
        showAddTask: Boolean
    },
    computed: {
        homePage() {
            if(this.$route.path === '/') {
                return true;
            } else {
                return false;
            }
        }
    }
}
</script>

<style lang="scss" scoped>

</style>