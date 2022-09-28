<template>
    <div>
        <textarea type="text" placeholder="Type something"  class="border border-1 border-gray-500 rounded-md text-2xl py-3 px-4" :value="textOutput"></textarea>
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
            textArray : [],
            textOutput: []
        }
    },
    watch: {
        textInput: function (newVal) {
            if(newVal == "backspace"){
                this.textArray.pop()
                this.textOutput = this.textArray.join('')
            }else if(newVal == "enter"){
                this.textArray.push(+ '\r\n' + '')
                this.textOutput = this.textArray.join('')
            }else{
                this.textArray.push(newVal)
                this.textOutput = this.textArray.join('')
            }
        }
    }

}
</script>

<style>

</style>