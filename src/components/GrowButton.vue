<template>
    <div @click="textClick"  class="disable-text-select grow md:h-8 lg:h-14 xl:h-16 flex justify-center items-center rounded lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer" :class="{ 'bg-gray-300': toggleButton}" @click.right.prevent>
        <div class="text-gray-900 text-sm lg:text-xl">
            {{value}}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: String,
        keyCode: String,
    },
    data() {
        return {
            toggleButton: false,
            keyPressed: ''
        }
    },
    methods: {
        textClick() {
            this.$emit('input-text', this.value)
        },
        setToggle(e) {
            let buttonCode = e.keyCode
            if (buttonCode == this.keyCode) {
                this.toggleButton = true
            }
        },
        resetToggle(e) {
            let buttonCode = e.keyCode
            if (buttonCode == this.keyCode) {
                this.toggleButton = false
            }
        }

    },
    created() {
        window.addEventListener('keydown', this.setToggle);
        window.addEventListener('keyup', this.resetToggle);
    },
    destroyed() {
        window.removeEventListener('keydown', this.setToggle);
    },

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