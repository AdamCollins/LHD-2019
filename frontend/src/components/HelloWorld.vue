<template lang="pug">
.hello
  h1 {{ msg }}
  .button(v-if="!showCamera", @click="buttonClicked")
    p Click Me!
  camera(v-if="showCamera")
</template>

<script>
// eslint-disable 
import Camera from './Camera'
export default {
  name: 'HelloWorld',
  components: {
    Camera
  },
  data() {
    return {
      msg: 'Insert Title Here',
      showCamera: false
    }
  },
  methods: {
    buttonClicked() {
      this.showCamera = true
    }
  }
}
</script>

<style lang="scss" scoped>
.button {
  width: 120px;
  height : 50px;
  background-color: lightskyblue;
  border-radius: 5px;
  align-self: center;

  &:hover {
    cursor: pointer;
  }
}
.hello {
  display: flex;
  flex-direction: column;
}
</style>
