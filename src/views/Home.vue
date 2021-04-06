<template>
  <div id="app">
    <!-- catching the emit with v-on -->
    <AddTodo v-on:add-todo="addTodo" />
    <!-- v-on listening for an event, del-todo was passed up via $emit from todos.vue -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [
        // this was our old hard coded ToDos
        // {
        //   id: 1,
        //   title: "Todo One",
        //   completed: false,
        // },
        // {
        //   id: 2,
        //   title: "Todo Two",
        //   completed: true,
        // },
        // {
        //   id: 3,
        //   title: "Todo Three",
        //   completed: false,
        // },
      ],
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        // filter returning each todo where our id is not equal to the id we passed up
        .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
      // this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodo(newTodo) {
      // destructuring these fields from our object we passed up in AddToDo
      const { title, completed } = newTodo;

      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title: title,
          completed: completed,
        })
        // adding our data to the server AND the UI
        // copy what is in todos with ...spread
        // we then are adding the response from the post
        // (the response gives us back that todo along with the id it created for us)
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
      // this was from when we passed in hardcoded data
      // this.todos = [...this.todos, newTodo];
    },
  },
  //created is similar to componentDidMount
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=10")
      // setting our todos array = to our response data
      .then((res) => (this.todos = res.data))
      .then((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
