<template>
  <div class="flex justify-center mt-40">
    <TextField  :textInput="input" />
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
      input: 'Yooo'
    }
  },
  methods: {
    onClickChild(value) {
      this.input = value
    }
  }

}

</script>

<style scoped>

</style>
