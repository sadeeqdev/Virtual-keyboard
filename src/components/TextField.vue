<template>
    <div class="border border-1 border-gray-400 rounded py-0 my-0" :class="{ 'border-gray-800 outline-3': setFocus}">
        <textarea 
            type="text" 
            placeholder="Type something"  
            class="w-11/12 lg:w-96 h-40 rounded-md text-2xl py-3 px-4 outline-0 border-0" 
            v-model="value" 
            v-on:focusin="setFocus = true"
            ref="textfield" 
            autocorrect="no"
            autocomplete="no"
            @change="setInput"></textarea>
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
            setFocus: false
        }
    },
    methods:{
        checkTextfield() {
                this.$refs.textfield.focus()
        },
        setInput(){
            this.value = this.value
            this.$emit('keyBoardSwitch', this.value)
        }
    },
    watch: {
        textInput: function (newVal) {
            this.value = newVal
        },
        value: function (val) {
            if (val.length > 0) {
                this.checkTextfield()
            }
        }
    },
    created() {
        window.addEventListener('keypress', this.removeChar);
    },
    destroyed() {
        window.removeEventListener('keydown', this.removeChar);

    },
}
</script>
