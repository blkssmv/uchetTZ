<template>
  <div>
    <div v-for="todo in allTodoList" :key="todo.id">
      <TodoItem :todo="todo" />
    </div>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
import { mapGetters } from "vuex";

export default {
  components: {
    TodoItem
  },
  computed: {
    ...mapGetters(["allTodoList", "completed"])
  }
};
</script>

<style scoped>
</style>