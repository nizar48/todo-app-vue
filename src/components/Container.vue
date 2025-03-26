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
</script>

<template>
  <div class="max-w-2xl mx-auto mt-10 p-6 bg-white shadow-lg rounded-lg">
    <h1 class="text-3xl font-bold text-center mb-6">Todo List</h1>

    <InputComponent @new-todo="addTodo"/>

    <TodoList :todos="todos"/>

    <ControlButtons/>
  </div>
</template>
