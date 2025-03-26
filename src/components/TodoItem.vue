<script setup lang="ts">
import { CircleCheckBig, Trash2 } from 'lucide-vue-next';

const props = defineProps({
  todoId: Number,
  todoText: String,
})

const emit = defineEmits(['deleteTodo', 'toggleTodo'])

</script>

<template>
  <div class="flex space-x-2 border rounded-sm border-gray-300 flex-1 px-2 py-1 items-center">
    <div class="flex-1 my-auto">
      {{ todoText }}
    </div>
    <button class="bg-blue-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer">
      <CircleCheckBig/>
    </button>
    <button
        @click="$emit('deleteTodo', todoId)"
        class="bg-red-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer"
    >
      <Trash2/>
    </button>
  </div>

</template>
