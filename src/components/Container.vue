<script setup lang="ts">

import InputComponent from "./InputComponent.vue";
import TodoList from "./TodoList.vue";
import ControlButtons from "./ControlButtons.vue";
</script>

<template>
  <div class="max-w-2xl mx-auto mt-10 p-6 bg-white border border-gray-200 shadow rounded-lg">
    <h1 class="text-3xl font-bold text-center mb-6">Todo List</h1>
    <InputComponent/>
    <TodoList/>
    <ControlButtons/>
  </div>
</template>
