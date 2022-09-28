<template>
  <div class="flex justify-center mt-40">
    <TextField  :textInput="textOutput" @keyBoardSwitch="onKeyboardSwitch"/>
  </div>
  <KeyPad @clicked-keyboard="onClickButton" :keyboardValue="keyboardValue"/>
</template>

<script>
   
import KeyPad from './components/KeyPad.vue';
import TextField from './components/TextField.vue';

export default {
  components: { TextField, KeyPad },
  data(){
    return {
      textOutput: '',
      keyboardValue: ''
    }
  },
  methods: {
    onClickButton(value) {
      this.textOutput = value
    },
    onKeyboardSwitch(value) {
      this.textOutput = value
      this.keyboardValue = value
    }
  }

}
</script>

