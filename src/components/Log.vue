<template>
  <div class="log">
      <div
      v-for="item in data"
      :key="item.id"
      class="log__item"
      >
        <p class="log__text">
          ID: {{item.id}},
        </p>
        <p class="log__text">
          Создан в: {{item.date}},
        </p>
        <p class="log__text">
          Тип: {{item.description}}
        </p>
        <button class="button button_remove" @click="$emit('buttonClick', item, item.id)">Удалить</button>
      </div>
    </div>
</template>

<script>
export default {
  props: {
    data: Array
  },
}
</script>

<style>
.log {
  width: 15%;
  max-height: 500px;
  border: 1px solid black;
  overflow-y: auto;
}

.log__item {
  display: flex;
  flex-direction: column;
  gap: 5px;
  align-items: center;
  padding: 5px 0;
  outline: 1px solid black;
}

.log__text {
  margin: 0;
}
</style>