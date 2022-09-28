<template>
    <div @click="textClick" class="disable-text-select h-6 w-5 md:w-8 md:h-8 lg:w-14 lg:h-14 xl:w-16 xl:h-16 shrink flex justify-center items-center rounded-md lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer" :class="{ 'bg-gray-400': toggleButton}" @click.right.prevent>
        <div class="text-gray-900 text-sm lg:text-2xl">    
            <div v-if="shiftValue == false">
                {{value.lowercase}}
            </div>
            <div v-if="shiftValue == true">
                {{value.uppercase}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: Object,
        checkShift: Boolean
    },
    data(){
        return{
            shiftValue: this.checkShift,
            toggleButton: false
        }
    },
    methods:{
        textClick(){
            if(this.checkShift){
                this.$emit('input-text', this.value.uppercase)
            }else{
                this.$emit('input-text', this.value.lowercase)
            }
        },
        doCommand(e) {
            let cmd = String.fromCharCode(e.keyCode).toLowerCase();
            if ((this.shiftValue == false && cmd === this.value.lowercase) || ((this.shiftValue == true) && (cmd === this.value.uppercase || cmd === this.value.lowercase))){
                this.toggleButton = true
                setTimeout(() => {
                    this.toggleButton = false
                }, 150)
            }
        }
    },
    watch: {
        checkShift: function (newVal) {
            this.shiftValue = newVal
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