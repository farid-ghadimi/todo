<template>
  <div>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @delete-todo="handleDelete"
      @mark-complete="handleMark"
    />
  </div>
</template>
  
<script setup>
import TodoItem from '~/components/ToDoItem.vue'
  
const props = defineProps({
  todos: {
    type: Array,
    required: true,
  }
})
  
const emit = defineEmits(['delete-todo', 'mark-complete'])

const handleDelete = (id) => {
  emit('delete-todo', id)
}

const handleMark = (id) => {
  emit('mark-complete', id)
}
</script>
  