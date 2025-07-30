<!-- data是放在App.vue這裡 -->

<script setup>
import ToDoItem from './components/ToDoItem.vue'
import ToDoForm from './components/ToDoForm.vue'
import { nanoid } from 'nanoid'
import { ref, computed } from 'vue'

const ToDoItems = ref([
  { id: 'todo-' + nanoid(), label: '買生椰拿鐵 🧉☕', done: true },
  { id: 'todo-' + nanoid(), label: '寫作業', done: false },
  { id: 'todo-' + nanoid(), label: '運動1小時', done: false },
  { id: 'todo-' + nanoid(), label: '洗力 🛁🧼', done: true },
  { id: 'todo-' + nanoid(), label: '帶力去公園 🐕🌼', done: true }
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

function editTodo({ id, label }) {
  const todo = ToDoItems.value.find(item => item.id === id)
  if (todo) todo.label = label
}

function deleteTodo(id) {
  ToDoItems.value = ToDoItems.value.filter(item => item.id !== id)
}

const completedCount = computed(() => ToDoItems.value.filter(item => item.done).length)
const totalCount = computed(() => ToDoItems.value.length)
</script>

<template>
  <div>
    <h2>代辦清單</h2>
    <ToDoForm @add="addTodo" />
    <div style="margin: 20px 0 20px 0; font-size: 20px; color: lightpink;">
      *´¨`*•.¸¸.•*´¨`*•.¸¸.•*´¨`* 完成紀錄 {{ completedCount }} / {{ totalCount }}   *´¨`*•.¸¸.•*´¨`*•.¸¸.•*´¨`*
    </div>
    <div
      v-for="item in ToDoItems"
      :key="item.id"
      style="margin-bottom: 18px;
      font-size: 20px;"
    >
      <ToDoItem
        :id="item.id"
        :label="item.label"
        :done="item.done"
        @change="updateTodoStatus"
        @edit="editTodo"
        @delete="deleteTodo"
      />
    </div>
  </div>
</template>
