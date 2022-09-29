<template>
  <div class="xl-10 mt-10 lg:mt-16 text-md flex justify-between lg:justify-center relative mx-5 lg:mx-20">
      <div class="text-xl lg:text-4xl font-meduim">Virtual Keyboard</div>
      <button class="flex lghidden absolute right-5 rounded bg-green-600 text-white px-4 py-2" @click="showKeyBoard">Toggle</button>
      <button class="hidden lg:flex absolute right-5 rounded bg-green-600 text-white px-4 py-2" @click="showKeyBoard">Toggle Keyboard</button>
  </div>
  <div class="flex justify-center mt-10 xl:mt-16" @click="toggleKeyboard = true">
    <TextField :textInput="textOutput" @keyBoardSwitch="onKeyboardSwitch"/>
  </div>
  <div v-show="toggleKeyboard">
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

