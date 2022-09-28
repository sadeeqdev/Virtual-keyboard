<template>
    <div @click="textClick"  class="disable-text-select grow md:h-8 lg:h-14 xl:h-16 flex justify-center items-center rounded lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer" @click.right.prevent>
        <div class="text-gray-900 text-sm lg:text-xl">
            {{value}}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: String
    },
    methods: {
        textClick() {
            this.$emit('input-text', this.value)
        }
    }
}
</script>

<style scoped>
.disable-text-select {
    user-select: none;
    -moz-user-select: none;
    -webkit-user-select: none;
    -ms-user-select: none;
}
</style>