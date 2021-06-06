<template>
  <div class="buttons-container">
        <div
          v-for="item in buttons"
          :key="item"
          @click="$emit('buttonClick', item)"
          class="button">
            Добавить {{item}}
        </div>
    </div>
</template>

<script>
export default {
  props: {
    buttons: Array
  }
}
</script>

<style>
.button {
  border: 1px solid black;
  cursor: pointer;
}
</style>