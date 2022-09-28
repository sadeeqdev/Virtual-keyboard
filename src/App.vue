<template>
  <div class="flex justify-center mt-40">
    <TextField  :textInput="textOutput" />
  </div>
  <KeyPad @clicked-keyboard="onClickChild"/>
</template>

<script>
   
import KeyPad from './components/KeyPad.vue';
import TextField from './components/TextField.vue';

export default {
  components: { TextField, KeyPad },
  data(){
    return {
      textArray: [],
      textOutput: ''
    }
  },
  methods: {
    onClickChild(value) {
      if (value == "backspace") {
        this.textArray.pop()
        this.textOutput = this.textArray.join('')
      } else if (value == "enter") {
        this.textArray.push('\r\n')
        this.textOutput = this.textArray.join('')
      } else if (value == "tab") {
        this.textArray.push('      ')
        this.textOutput = this.textArray.join('')
      }
      else {
        this.textArray.push(value)
        this.textOutput = this.textArray.join('')
      }
    }
  }

}

</script>

<style scoped>

</style>
