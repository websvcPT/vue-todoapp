<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos">
      <TodoItem
        v-bind:todo="todo"
        v-on:del-todo="$emit('del-todo', todo.id)"
        v-on:update-todo="$emit('update-todo', todo.id, updtTodo)"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
  name: 'Todos',
  props: ['todos'],
  components: {
    TodoItem
  }
};
</script>

<style scoped>
</style>
