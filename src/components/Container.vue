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
    completed: false
  })
}

const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
}

const toggleTodo = (id) => {
  const todo = todos.value.find(todo => todo.id === id)
  if (todo) {
    todo.completed = !todo.completed
  }
}

const filteredTodos = computed(() => {
  switch (filter.value) {
    case 'active':
      return todos.value.filter(todo => !todo.completed)
    case 'completed':
      return todos.value.filter(todo => todo.completed)
    default:
      return todos.value
  }
})

const clearCompleted = () => {
  todos.value = todos.value.filter(todo => !todo.completed)
}
</script>

<template>
  <div class="max-w-2xl mx-auto mt-10 p-6 bg-white shadow-lg rounded-lg">
    <h1 class="text-3xl font-bold text-center mb-6">Todo List</h1>

    <InputComponent @new-todo="addTodo"/>

    <TodoList
        :todos="filteredTodos"
        @delete-todo="deleteTodo"
        @toggle-todo="toggleTodo"
    />

    <ControlButtons
        :todos="todos"
        @filter="filter = $event"
        @clear-completed="clearCompleted"
    />
  </div>
</template>
