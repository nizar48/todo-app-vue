<script setup lang="ts">

import { ref } from "vue";

const text = ref("")

const emit = defineEmits(["newTodo"])

const handleClick = () => {
  if (!text.value.trim()) return
  emit("newTodo", text.value.trim())
  text.value = "";
}
</script>

<template>
  <div class="flex items-center space-y-3 md:space-y-0 lg:space-x-4 flex-col md:flex-row md:space-x-8 mb-4">
    <input
        class="px-2 py-1 border border-gray-300 rounded-md flex-1 w-full focus:outline-none focus:ring-2 focus:ring-blue-500"
        placeholder="Type your todo here.."
        v-model="text"
        @keyup.enter="handleClick"
    />
    <button class="bg-slate-900 hover:opacity-95 py-1 w-24 px-3 rounded-md text-white cursor-pointer"
            @click="handleClick"
    >
      Add todo
    </button>
  </div>
</template>
