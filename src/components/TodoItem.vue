<script setup lang="ts">
import type Todo from '@/models/Todo'

const props = defineProps<{
  todo: Todo
}>()
const emit = defineEmits<{
  (event: 'toggle', id: string): void
  (event: 'delete', id: string): void
}>()

const handleToggle = () => emit('toggle', props.todo.id)
const handleDelete = () => emit('delete', props.todo.id)
</script>

<template>
  <li>
    <input type="checkbox" :checked="props.todo.completed" @click="handleToggle" />
    <span :class="props.todo.completed && 'done'" @click="handleToggle">{{
      props.todo.title
    }}</span>
    <button @click="handleDelete">X</button>
  </li>
</template>

<style scoped>
li {
  display: flex;
  flex-direction: row;
  align-items: center;
  margin-bottom: 1rem;
  gap: 1rem;
}

li input[type='checkbox'] {
  width: 1rem;
  height: 1rem;
}

li span {
  flex: 1;
}

.done {
  text-decoration: line-through;
}
</style>
