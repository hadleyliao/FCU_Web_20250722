<template>
  <form @submit.prevent="handleSubmit">
    <label for="todo-input">請輸入代辦事項：</label>
    <input
      id="todo-input"
      type="text"
      v-model.lazy.trim="inputValue"
      autocomplete="off"
    />
    <button type="submit">新增</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
const inputValue = ref('')
const emit = defineEmits(['add'])

function handleSubmit() {
  if (inputValue.value) {
    emit('add', inputValue.value)
    inputValue.value = ''
  }
}
</script>
