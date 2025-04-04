<template>
  <div
      class="flex items-center justify-between p-2 border-b hover:bg-gray-100"
  >
    <div
      class="cursor-pointer flex-1"
      :class="{ 'line-through text-gray-500': todo.completed }"
      @click="markComplete"
    >
      {{ todo.text }}
    </div>
    <button
      @click="deleteTodo"
      class="text-red-500 hover:text-red-700 transition-colors"
    >
      Delete
    </button>
  </div>
</template>
  
<script setup>
const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
})
  
const emit = defineEmits(['delete-todo', 'mark-complete'])
  
const markComplete = () => {
  emit('mark-complete', props.todo.id)
}
  
const deleteTodo = () => {
  emit('delete-todo', props.todo.id)
}
</script>
  