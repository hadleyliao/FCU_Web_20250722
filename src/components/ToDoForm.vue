<template>
  <form @submit.prevent="handleSubmit">
    <label for="todo-input">請輸入代辦事項：</label>
    <input
      id="todo-input"
      type="text"
      v-model.lazy.trim="label"
      autocomplete="off"
    />
    <button type="submit">新增</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
const label = ref('')

function handleSubmit() {
  if (label.value) {
    emit('add', label.value)
    label.value = ''
  }
}

const emit = defineEmits(['add'])
</script>
