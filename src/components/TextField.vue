<template>
    <div>
        <textarea type="text" placeholder="Type something"  class="border border-1 border-gray-500 rounded-md text-2xl py-3 px-4" v-model="value" ref="textfield" @change="setInput"></textarea>
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
