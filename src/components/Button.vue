<template>
    <div @click="textClick" class="disable-text-select h-6 w-5 md:w-8 md:h-8 lg:w-14 lg:h-14 xl:w-16 xl:h-16 shrink flex justify-center items-center rounded-md lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer" @click.right.prevent>
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
    },
    watch: {
        checkShift: function (newVal) {
            this.shiftValue = newVal
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