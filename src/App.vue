<script setup>
import TodoItem from './components/TodoItem.vue'
import ToDoForm from './components/ToDoForm.vue'
import { nanoid } from 'nanoid'
import { ref } from 'vue'

const ToDoItems = ref([
  { id: 'todo-' + nanoid(), label: '買牛奶', done: false },
  { id: 'todo-' + nanoid(), label: '寫作業', done: true },
  { id: 'todo-' + nanoid(), label: '運動30分鐘', done: false },
  { id: 'todo-' + nanoid(), label: '閱讀10頁', done: false }
])

function addTodo(label) {
  ToDoItems.value.push({
    id: 'todo-' + nanoid(),
    label,
    done: false
  })
}
</script>

<template>
  <div>
    <h2>代辦清單</h2>
    <ToDoForm @add="addTodo" />
    <TodoItem
      v-for="item in ToDoItems"
      :key="item.id"
      :id="item.id"
      :label="item.label"
      :done="item.done"
    />
  </div>
</template>
