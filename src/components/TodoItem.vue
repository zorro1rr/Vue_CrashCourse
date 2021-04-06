<template>
  <!-- here is the syntax for passing a conditional class -->
  <div class="todo-item" v-bind:class="{ 'is-complete': todo.completed }">
    <p>
      <!-- v-on used for adding events, here listening for changes -->
      <!-- on change we are running the markComplete method we defined in our script JS -->
      <input type="checkbox" v-on:change="markComplete" />
      {{ todo.title }}
      <!-- On click event we pass up our id via $emit named as del-todo -->
      <button class="del" @click="$emit('del-todo', todo.id)">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      // setting completed to whatever is is NOT
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>
