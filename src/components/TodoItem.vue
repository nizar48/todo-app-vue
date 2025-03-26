<script setup>
import { ref } from 'vue'
import { CircleCheckBig, Trash2, Edit2, Check, X } from 'lucide-vue-next';

const props = defineProps({
  todoId: Number,
  todoText: String,
  completed: {
    type: Boolean,
    default: false
  },
  isEditing: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits([
  'deleteTodo',
  'toggleTodo',
  'startEdit',
  'updateTodo',
  'cancelEdit'
])

const editText = ref(props.todoText)

const handleUpdate = () => {
  if (editText.value.trim()) {
    emit('updateTodo', {
      id: props.todoId,
      newText: editText.value
    })
  }
}
</script>

<template>
  <div
      v-if="!isEditing"
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
        @click="$emit('startEdit', todoId)"
        class="bg-yellow-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer"
    >
      <Edit2/>
    </button>
    <button
        @click="$emit('deleteTodo', todoId)"
        class="bg-red-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer"
    >
      <Trash2/>
    </button>
  </div>
  
  <div
      v-else
      class="flex space-x-2 border rounded-sm border-gray-300 flex-1 px-2 py-1 items-center"
  >
    <input
        v-model="editText"
        class="flex-1 px-2 py-1 border rounded"
        @keyup.enter="handleUpdate"
        @keyup.esc="$emit('cancelEdit')"
        ref="editInput"
    />
    <button
        @click="handleUpdate"
        class="bg-green-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer"
    >
      <Check/>
    </button>
    <button
        @click="$emit('cancelEdit')"
        class="bg-red-500 text-white h-8 w-8 rounded-sm flex justify-center items-center cursor-pointer"
    >
      <X/>
    </button>
  </div>
</template>
