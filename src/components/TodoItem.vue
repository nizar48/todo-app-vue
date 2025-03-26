<script setup>
import { CircleCheckBig, Trash2 } from 'lucide-vue-next';

const props = defineProps({
  todoId: Number,
  todoText: String,
  completed: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['deleteTodo', 'toggleTodo'])
</script>

<template>
  <div
      class="flex space-x-2 border rounded-sm border-gray-300 flex-1 px-2 py-1 items-center"
      :class="{ 'bg-gray-100': completed }"
  >
    <div
        class="flex-1 my-auto"
        :class="{ 'line-through text-gray-500': completed }"
    >
      {{ todoText }}
    </div>
    <button
        @click="$emit('toggleTodo', todoId)"
        class="bg-blue-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer"
        :class="{ 'bg-green-500': completed }"
    >
      <CircleCheckBig :class="{ 'text-white': completed }"/>
    </button>
    <button
        @click="$emit('deleteTodo', todoId)"
        class="bg-red-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer"
    >
      <Trash2/>
    </button>
  </div>
</template>