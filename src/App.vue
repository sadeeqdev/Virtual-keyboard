<template>
  <div class="flex justify-center mt-40">
    <TextField  :textInput="input" />
  </div>
  <KeyPad @clicked="onClickChild"/>
</template>

<script>

import KeyPad from './components/KeyPad.vue';
import TextField from './components/TextField.vue';

export default {
  components: { TextField, KeyPad },
  data(){
    return {
      input: 'Yooo'
    }
  },
  methods: {
    onClickChild(value) {
      console.log("hello")
    }
  }

}

</script>

<style scoped>

</style>
