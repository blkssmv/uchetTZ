<template>
  <div class="col container">
    <input
        v-model="todoTitle"
        class="todo-title form-control mb-3"
        type="text"
        placeholder="Title"
    />
    <textarea
        v-model="todoText"
        class="todo-text form-control mb-3"
        type="text"
        placeholder="Description"
    />
    <label for="deadline">
      <h5>Deadline</h5>
    </label>
    <input
        id="deadline"
        v-model="todoDeadline"
        class="todo-title form-control mb-2"
        type="date"
    />
    <button @click="addTodoI" class="btn btn-primary">Add</button>
  </div>
</template>

<script>
import {mapActions} from "vuex";
import {v1} from "uuid";

export default {
  data() {
    return {
      todoTitle: "",
      todoText: "",
      todoDeadline: ""
    };
  },
  methods: {
    ...mapActions(["addTodo"]),
    addTodoI() {
      this.addTodo({
        id: v1(),
        title: this.todoTitle,
        text: this.todoText,
        deadline: this.todoDeadline,
        complete: false
      });
      this.todoTitle = "";
      this.todoText = "";
      this.todoDeadline = "";
    }
  }
};
</script>

<style scoped>
</style>