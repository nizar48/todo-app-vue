<script setup lang="ts">

import TodoItem from "./TodoItem.vue";

const props = defineProps({
  todos: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['deleteTodo', 'toggleTodo'])
</script>

<template>
  <div class="p-2 border border-gray-300 shadow rounded-md w-sm mr-4  lg:w-[39rem] min-h-60 space-y-2">
    <template v-if="todos.length">
      <TodoItem
          v-for="todo in todos"
          :key="todo.id"
          :todo-text="todo.text"
          :todo-id="todo.id"
          @delete-todo="$emit('deleteTodo', $event)"
      />
    </template>
    <p v-else class="text-center text-gray-500">
      No todos yet. Add a new todo!
    </p>
  </div>
</template>
