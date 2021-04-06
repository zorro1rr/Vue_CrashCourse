<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="Add Todo..."
      />
      <input type="submit" value="Submit" class="btn" />
    </form>
  </div>
</template>

<script>
// import uuid npm package that allows us to create ids on the fly
// import uuid from "uuid";
export default {
  name: "AddTodo",
  data() {
    return {
      // we bound this to our v-model name to pass our input field content through
      title: "",
    };
  },
  methods: {
    // passing event(e) parameter
    addTodo(e) {
      // preventing default so some doesn't submit to a file
      e.preventDefault();
      const newTodo = {
        // creating a unique id with uuid - we got rid of this because jsonplaceholders todo already have an id
        // id: uuid.v4(),
        // we have access to this.title because it is bound in our data return object
        title: this.title,
        completed: false,
      };
      // Send up to parent
      this.$emit("add-todo", newTodo);

      // clears our title(input field) after we submit
      this.title = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
input[type="submit"] {
  flex: 2;
}
</style>
