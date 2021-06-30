<template>
  <div id="app">
    <VCanvas :canvas-id="'canvas-one'" ref="childCanvas"/>
    <button id="link" @click="saveImage">SAVE</button>
  </div>
</template>

<script>
import VCanvas from '@/components/VCanvas'

export default {
  name: 'App',
  components: {
    VCanvas
  },
  data: () => ({
  }),
  methods: {
    saveImage() {
        const canvas = document.getElementById('canvas-one');
        const data = canvas.toDataURL('image/png').replace("image/png", "image/octet-stream");
        window.open(data)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
