<template>
  <div>
    <div class="row my-3 justify-content-between align-items-center">
      <div v-if="!editing">
        <h4>Task: {{ todo.title }}</h4>
        <h4>Description: {{ todo.text }}</h4>
        <h4>Deadline: {{ todo.deadline }}</h4>
      </div>


      <div v-else class="mr-2 row justify-content-between align-items-center col">
        <input
            v-model="todoTitle"
            type="text"
            class="form-control mb-3"
        />
        <textarea
            v-model="todoText"
            rows="1"
            type="text"
            class="form-control mb-3"
        />
        <input
            id="deadline"
            v-model="todoDeadline"
            class="todo-title form-control mb-2"
            type="date"
        />
        <div>
          <input :checked="completed" class="mr-1" @change="onCompleted" type="checkbox"/>
          <label class="m-0">Completed</label>
        </div>
      </div>
      <div class="row align-items-center">
        <button @click="updateTodoI(todo)" class="btn btn-primary mx-2">{{ editing ? 'Update' : 'Edit' }}</button>
        <button @click="deleteTodo(todo.id)" class="btn btn-danger">Delete</button>
      </div>
    </div>
  </div>
</template>

<script>
import {mapActions} from "vuex";

export default {
  props: {
    todo: {}
  },
  data() {
    return {
      todoTitle: "",
      todoText: "",
      todoDeadline: "",
      editing: false,
      completed: false
    };
  },
  methods: {
    ...mapActions(["deleteTodo", "updateTodo", "changeCompleted"]),
    onCompleted() {
      this.completed = this.completed !== true;
    },
    updateTodoI(todo) {
      this.editing = this.editing !== true;
      if (this.editing) {
        this.todoTitle = todo.title;
        this.todoText = todo.text;
        this.todoDeadline = todo.deadline;
        this.updateTodo(todo);
      } else {
        todo.title = this.todoTitle;
        todo.text = this.todoText;
        todo.deadline = this.todoDeadline;
        todo.complete = this.completed;
        this.changeCompleted();
      }
    }
  }
};
</script>

<style scoped>
</style>