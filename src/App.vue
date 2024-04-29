<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: true },
  { id: id++, text: 'Learn JavaScript', done: true },
  { id: id++, text: 'Learn Vue', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <div class="container mx-auto bg-gray-200 rounded-xl shadow border p-8 m-10">
      <div class="text-center">
          <h1 class="text-3xl font-bold pb-4">List Kegiatan</h1>
      </div>
      <div>
          <form @submit.prevent="addTodo">
          <input class="shadow-lg rounded-md border " v-model="newTodo">
          <button class="px-3">
            <span class="material-symbols-outlined">
task_alt 
</span>confirm
          </button>
          <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@NaN,0,0,0" />
      </form>
      </div>
      <ul>
  <li v-for="todo in filteredTodos" :key="todo.id">
    <input type="checkbox" v-model="todo.done">
    <span :class="{ done: todo.done }">{{ todo.text }}</span>
    <button @click="removeTodo(todo)">
      <span class="material-symbols-outlined">delete_forever</span>
    </button>
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20,600,0,-25" />
  </li>
</ul>
<button @click="hideCompleted = !hideCompleted">
  {{ hideCompleted ? 'Show all' : 'Hide completed' }}
</button>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
} 
</style>
<style>
@import "style.css";
</style>