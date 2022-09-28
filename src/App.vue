<template>
  <div class="flex justify-center mt-40">
    <TextField  :textInput="textOutput" />
  </div>
  <KeyPad @clicked-keyboard="onClickButton"/>
</template>

<script>
   
import KeyPad from './components/KeyPad.vue';
import TextField from './components/TextField.vue';

export default {
  components: { TextField, KeyPad },
  data(){
    return {
      textOutput: ''
    }
  },
  methods: {
    onClickButton(value) {
      this.textOutput = value
    }
  }

}

</script>

<style scoped>

</style>
