<template>
  <div class="flex justify-center mt-40">
    <TextField  :textInput="textAreaInput" />
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
      textAreaInput: ''
    }
  },
  methods: {
    onClickChild(value) {
      this.textAreaInput = value
    }
  }

}

</script>

<style scoped>

</style>
