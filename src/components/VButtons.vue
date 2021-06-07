<template>
  <div class="buttons">
    <div
      v-for="item in buttons"
      :key="item.i"
      class="buttons__item"
    >
      <img class="buttons__image" :src="item.image" alt="Фигура">
      {{item.type}}
      <button class="button" @click="$emit('buttonClick', item.type)">Добавить</button>
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

.buttons__item {
  display: flex;
  gap: 5px;
  flex-direction: column;
  padding: 10px;
  align-items: center;
  border: 1px solid black;
}

.buttons__image {
  width: 20px;
  height: 20px;
}

.button {
  cursor: pointer;
}
</style>