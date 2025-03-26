<script setup>
import { computed } from 'vue'

const props = defineProps({
  todos: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['filter', 'clearCompleted'])

const activeCount = computed(() =>
    props.todos.filter(todo => !todo.completed).length
)

const hasCompleted = computed(() =>
    props.todos.some(todo => todo.completed)
)
</script>

<template>
  <div class="flex justify-between items-center mt-4 p-2 border-t border-gray-200">
    <span class="text-sm text-gray-600">
      {{ activeCount }} item{{ activeCount !== 1 ? 's' : '' }} left
    </span>

    <div class="space-x-2">
      <button
          @click="$emit('filter', 'all')"
          class="text-sm text-gray-600 hover:text-black"
      >
        All
      </button>
      <button
          @click="$emit('filter', 'active')"
          class="text-sm text-gray-600 hover:text-black"
      >
        Active
      </button>
      <button
          @click="$emit('filter', 'completed')"
          class="text-sm text-gray-600 hover:text-black"
      >
        Completed
      </button>
    </div>

    <button
        v-if="hasCompleted"
        @click="$emit('clearCompleted')"
        class="text-sm text-red-500 hover:text-red-700"
    >
      Clear Completed
    </button>
  </div>
</template>