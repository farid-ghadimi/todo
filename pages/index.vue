<template>
  <div class="mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold mb-4 text-center">Todo List</h1>
    <TodoForm @add-todo="handleAddTodo"/>
    <TodoList
      :todos="todos"
      @delete-todo="handleDeleteTodo"
      @mark-complete="handleMarkTodo"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import TodoForm from '~/components/ToDoForm.vue'
import TodoList from '~/components/ToDoList.vue'

const todos = ref([])

onMounted(() => {
  const storedTodos = localStorage.getItem('todos')
  if (storedTodos) {
    todos.value = JSON.parse(storedTodos)
  }
})

watch(
  todos,
  (newTodos) => {
    localStorage.setItem('todos', JSON.stringify(newTodos))
  },
  { deep: true }
)

const handleAddTodo = (todoText) => {
  todos.value.push({
    id: Date.now(),
    text: todoText,
    completed: false,
  })
}

const handleDeleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}

const handleMarkTodo = (id) => {
  const todo = todos.value.find((todo) => todo.id === id)
  if (todo) {
    todo.completed = !todo.completed
  }
}
</script>
