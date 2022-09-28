<template>
    <div>
        <textarea type="text" placeholder="Type something"  class="border border-1 border-gray-500 rounded-md text-2xl py-3 px-4" :value="value"></textarea>
    </div>
</template>

<script>
export default {
    props: {
        textInput: String
    },
    data(){
        return{
            value: this.textInput,
        }
    },
    watch: {
        textInput: function (newVal) {
            this.value = newVal
        }
    }
}
</script>
