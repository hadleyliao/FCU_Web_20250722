<script setup>
import ToDoItem from './components/ToDoItem.vue'
import ToDoForm from './components/ToDoForm.vue'
import { nanoid } from 'nanoid'
import { ref, computed } from 'vue'

const ToDoItems = ref([
  { id: 'todo-' + nanoid(), label: '買生椰拿鐵🧉', done: true },
  { id: 'todo-' + nanoid(), label: '寫作業', done: false },
  { id: 'todo-' + nanoid(), label: '運動30分鐘', done: false },
  { id: 'todo-' + nanoid(), label: '遛狗 🐕', done: true }
])

function addTodo(label) {
  ToDoItems.value.push({
    id: 'todo-' + nanoid(),
    label,
    done: false
  })
}

function updateTodoStatus({ id, done }) {
  const todo = ToDoItems.value.find(item => item.id === id)
  if (todo) todo.done = done
}

const completedCount = computed(() => ToDoItems.value.filter(item => item.done).length)
const totalCount = computed(() => ToDoItems.value.length)
</script>

<template>
  <div>
    <h2>代辦清單</h2>
    <ToDoForm @add="addTodo" />
    <div style="margin: 8px 0; color: #888;">
      ---------------完成紀錄 {{ completedCount }} / {{ totalCount }}---------------
    </div>
    <ToDoItem
      v-for="item in ToDoItems"
      :key="item.id"
      :id="item.id"
      :label="item.label"
      :done="item.done"
      @change="updateTodoStatus"
    />
  </div>
</template>
