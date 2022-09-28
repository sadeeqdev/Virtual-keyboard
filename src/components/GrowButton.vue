<template>
    <div @click="textClick"  class="disable-text-select grow md:h-8 lg:h-14 xl:h-16 flex justify-center items-center rounded lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer" :class="{ 'bg-gray-400': toggleButton}" @click.right.prevent>
        <div class="text-gray-900 text-sm lg:text-xl">
            {{value}}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: String,
    },
    data() {
        return {
            toggleButton: false
        }
    },
    methods: {
        textClick() {
            this.$emit('input-text', this.value)
        },
        doCommand(e) {
            let cmd = String.fromCharCode(e.keyCode).toLowerCase();
            console.log(e.keyCode)
            
            if (cmd === this.value) {
                this.toggleButton = true
                setTimeout(() => {
                    this.toggleButton = false

                }, 150)
            }
        }

    },
    created() {
        window.addEventListener('keypress', this.doCommand);
    },
    destroyed() {
        window.removeEventListener('keypress', this.doCommand);
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