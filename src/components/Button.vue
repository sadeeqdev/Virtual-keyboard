<template>
    <div @click="textClick" class="disable-text-select h-6 w-5 md:w-8 md:h-8 lg:w-14 lg:h-14 xl:w-16 xl:h-16 shrink flex justify-center items-center rounded-md lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer" :class="{ 'bg-gray-300': toggleButton}" @click.right.prevent>
        <div class="text-gray-900 text-sm lg:text-2xl">    
            <div v-if="shiftValue == false && capsValue == false">
                {{value.lowercase}}
            </div>
            <div v-if="shiftValue == true && capsValue == false" >
                {{value.uppercase}}
            </div>
            <div v-if="capsValue == true && shiftValue == true">
                {{value.uppercase}}
            </div>
            <div v-if="capsValue == true && shiftValue == false">
                {{value.uppercase}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: Object,
        checkShift: Boolean,
        checkCaps: Boolean
    },
    data(){
        return{
            shiftValue: this.checkShift,
            capsValue: this.checkCaps,
            toggleButton: false
        }
    },
    methods:{
        textClick(){
            if (this.shiftValue){
                this.$emit('input-text', this.value.uppercase)
            }else if(this.capsValue){
                this.$emit('input-text', this.value.uppercase)
            }else if (!this.capsValue) {
                this.$emit('input-text', this.value.lowercase)
            }else{
                this.$emit('input-text', this.value.lowercase)
            }
        },
        setToggle(e) {
            let cmd = e.key
            if ((this.shiftValue == false && cmd == this.value.lowercase) || ((this.shiftValue == true) && (cmd == this.value.uppercase || cmd == this.value.lowercase))){
                this.toggleButton = true
            }

            if(e.keyCode == 16){
                this.capsValue = false
                this.shiftValue = true
            }else if(e.keyCode == 20){
                this.capsValue = !this.capsValue
                this.shiftValue = false

            }
        },
        resetToggle(e) {
            let cmd = e.key
            if ((this.shiftValue == false && cmd == this.value.lowercase) || ((this.shiftValue == true) && (cmd == this.value.uppercase || cmd == this.value.lowercase))) {
                this.toggleButton = false
            }

            if (e.keyCode == 16) {
                this.shiftValue = false
                this.capsValue = false
            }
        }
    },
    watch: {
        checkShift: function (newVal) {
            this.shiftValue = newVal
        },
        checkCaps: function (newVal) {
            this.capsValue = newVal
        }
    },
    created() {
        window.addEventListener('keydown', this.setToggle);
        window.addEventListener('keyup', this.resetToggle);
    },
    destroyed() {
        window.removeEventListener('keydown', this.setToggle);
        window.removeEventListener('keyup', this.resetToggle);

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