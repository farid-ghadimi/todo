<template>
  <form
    @submit.prevent="addTodo"
    class="flex mb-4"
  >
    <input
      v-model="newTodo"
      placeholder="Add a new todo"
      class="flex-1 border rounded px-4 py-2 focus:outline-none focus:ring-2 focus:ring-blue-400"
    />
    <button
      type="submit"
      class="bg-blue-500 text-white rounded px-4 py-2 ml-2 hover:bg-blue-600 hover:cursor-pointer"
    >
    Add
    </button>
  </form>
</template>
  
<script setup>
  import { ref } from 'vue'
  
  const newTodo = ref('')
  
  const emit = defineEmits(['add-todo'])
  
  const addTodo = () => {
    if (newTodo.value !== '') {
      emit('add-todo', newTodo.value)
      newTodo.value = ''
    }
  }
</script>
  