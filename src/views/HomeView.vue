<script setup lang="ts">
import TodoItem from '@/components/TodoItem.vue'
import type Todo from '@/models/Todo'
import { ref, type Ref } from 'vue'

let newTodoInput: string = ''

const todoItems: Ref<Todo[]> = ref([])

const handleSubmit = () => {
  todoItems.value = [
    ...todoItems.value,
    {
      completed: false,
      title: newTodoInput,
      id: Math.random().toString()
    }
  ]
  newTodoInput = ''
}

const handleDelete = (id: string) => {
  todoItems.value = todoItems.value.filter((todoItem) => todoItem.id !== id)
}

const handleToggle = (id: string) => {
  todoItems.value = todoItems.value.map((todoItem) => {
    if (todoItem.id === id) {
      return {
        ...todoItem,
        completed: !todoItem.completed
      }
    }
    return todoItem
  })
}
</script>

<template>
  <main>
    <h1>Todo List</h1>
    <form @submit.prevent="handleSubmit" class="input-container">
      <input required type="text" placeholder="New Todo Item" v-model="newTodoInput" />
      <input type="submit" value="Create" />
    </form>
    <ul v-if="todoItems.length > 0">
      <TodoItem
        v-for="todoItem in todoItems"
        :todo="todoItem"
        :key="todoItem.id"
        delete
        @delete="handleDelete"
        @toggle="handleToggle"
      />
    </ul>
    <p v-else>No todo items yet</p>
  </main>
</template>

<style scoped>
main {
  margin: 4rem;
  display: flex;
  flex-direction: column;
}

.input-container {
  display: flex;
  flex-direction: row;
  /* background-color: blue; */
  align-items: center;
}

.input-container input[type='text'] {
  flex: 1;
  padding: 1rem;
}

ul {
  margin-top: 2rem;
  list-style: none;
  padding: 0;
}
</style>
