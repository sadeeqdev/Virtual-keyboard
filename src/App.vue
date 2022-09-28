<template>
  <div class="mt-5 text-3xl flex justify-center">
      <button class="rounded bg-slate-500 text-white px-4 py-2" @click="showKeyBoard">Toggle Keyboard</button>
  </div>
  <div class="flex justify-center mt-32" @click="toggleKeyboard = true">
    <TextField :textInput="textOutput" @keyBoardSwitch="onKeyboardSwitch"/>
  </div>
  <div v-if="toggleKeyboard">
      <KeyPad @clicked-keyboard="onClickButton" :keyboardValue="keyboardValue"/>
  </div>
</template>

<script>
   
import KeyPad from './components/KeyPad.vue';
import TextField from './components/TextField.vue';

export default {
  components: { TextField, KeyPad },
  data(){
    return {
      textOutput: '',
      keyboardValue: '',
      toggleKeyboard: false
    }
  },
  methods: {
    onClickButton(value) {
      this.textOutput = value
    },
    onKeyboardSwitch(value) {
      this.textOutput = value
      this.keyboardValue = value
    },
    showKeyBoard(){
      this.toggleKeyboard = !this.toggleKeyboard
    }
  }

}
</script>

