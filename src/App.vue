<template>
  <div id="app">
    <VCanvas :canvas-id="'canvas-one'" ref="childCanvas"/>
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
  })
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
