<template>
  <div>
    <!-- similar to for in loops that iterates through an object -->
    <!-- needs a key just like iterated children in React -->
    <div v-bind:key="todo.id" v-for="todo in todos">
      <!-- v-on listening for an event, del-todo was passed up via $emit from todoItem.vue -->
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "Todos",
  components: {
    TodoItem,
  },
  props: ["todos"],
};
</script>

<style scoped></style>
