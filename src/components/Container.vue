<script setup>
import { ref, computed } from 'vue'
import InputComponent from './InputComponent.vue'
import TodoList from './TodoList.vue'
import ControlButtons from './ControlButtons.vue'

const todos = ref([])
const filter = ref('all')
const editingTodoId = ref(null)

const addTodo = (text) => {
  todos.value.push({
    id: Date.now(),
    text,
    completed: false
  })
}

const deleteTodo = (id) => {
  todos.value = todos.value.filter(todo => todo.id !== id)
  // Cancel editing if deleted todo was being edited
  if (editingTodoId.value === id) {
    editingTodoId.value = null
  }
}

const toggleTodo = (id) => {
  const todo = todos.value.find(todo => todo.id === id)
  if (todo) {
    todo.completed = !todo.completed
  }
}

const startEditing = (id) => {
  editingTodoId.value = id
}

const updateTodo = (payload) => {
  const {id, newText} = payload
  const todo = todos.value.find(todo => todo.id === id)
  if (todo) {
    todo.text = newText.trim()
    editingTodoId.value = null
  }
}

const cancelEditing = () => {
  editingTodoId.value = null
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
  <div class="max-w-2xl mx-auto mt-10 p-6 bg-white shadow border border-gray-200 rounded-lg">
    <h1 class="text-3xl font-bold text-center mb-6">Todo List</h1>

    <InputComponent @new-todo="addTodo"/>

    <TodoList
        :todos="filteredTodos"
        :editing-todo-id="editingTodoId"
        @delete-todo="deleteTodo"
        @toggle-todo="toggleTodo"
        @start-edit="startEditing"
        @update-todo="updateTodo"
        @cancel-edit="cancelEditing"
    />

    <ControlButtons
        :todos="todos"
        @filter="filter = $event"
        @clear-completed="clearCompleted"
    />
  </div>
</template>