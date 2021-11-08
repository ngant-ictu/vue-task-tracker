<template>
    <button :style="{background: color}" @click="onClick" class="text-1xl text-white px-4 py-2 rounded hover:bg-green-600">{{ text }}</button>
</template>

<script>
export default {
    name: 'ButtonTask',
    props: {
        text: String,
        color: String
    },
    methods: {
        onClick() {
            this.$emit('toggle-add-task')
        }
    }
}
</script>

<style lang="scss">

</style>