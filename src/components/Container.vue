<script setup>
import { computed, ref } from 'vue'
import InputComponent from './InputComponent.vue'
import TodoList from './TodoList.vue'
import ControlButtons from './ControlButtons.vue'

const todos = ref([])
const filter = ref('all')

const addTodo = (text) => {
  todos.value.push({
    id: Date.now(),
    text,
  })
}

const deleteTodo = (id) => {
  console.log("deleteTodo called")

  todos.value = todos.value.filter(todo => todo.id !== id)
}
</script>

<template>
  <div class="max-w-2xl mx-auto mt-10 p-6 bg-white shadow border border-gray-200 rounded-lg">
    <h1 class="text-3xl font-bold text-center mb-6">Todo List</h1>

    <InputComponent @new-todo="addTodo"/>

    <TodoList :todos="todos" @delete-todo="deleteTodo"/>

    <ControlButtons/>
  </div>
</template>
