<template>
    <div @click="textClick" class="h-6 w-5 md:w-8 md:h-8 lg:w-14 lg:h-14 xl:w-16 xl:h-16 shrink flex justify-center items-center rounded-md lg:rounded-lg shadow-sm bg-gray-50 hover:bg-gray-200 hover:cursor-pointer">
        <div class="text-gray-900 text-sm lg:text-2xl">    
            {{value.lowercase}}
        </div>
    </div>
</template>

<script>
export default {
    props: {
        value: Object
    },
    methods:{
        textClick(){
            this.$emit('input-text', this.value.lowercase)
        }
    }

}
</script>

<style>

</style>