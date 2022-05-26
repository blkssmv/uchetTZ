<template>
  <div id="app">
    <HeaderComponent/>
    <div class="main-content container">
      <span v-if="isAuthorized">
        <TodoInput />
        <TodoStatus />
        <TodoList />
      </span>
      <span v-else>
        <RegisterComponent v-on:checkA="checkAuth()"/>
      </span>
    </div>
    <FooterComponent/>
  </div>
</template>

<script>
import TodoInput from "@/components/TodoInput";
import TodoList from "@/components/TodoList";
import TodoStatus from "@/components/TodoStatus";
import RegisterComponent from "@/components/RegisterComponent";
import HeaderComponent from "./components/HeaderComponent";
import FooterComponent from "@/components/FooterComponent";

export default {
  name: "App",
  components: {
    FooterComponent,
    HeaderComponent,
    TodoInput,
    TodoList,
    TodoStatus,
    RegisterComponent
  },
  data () {
    return {
      isAuthorized: false
    }
  },
  created() {
    this.checkAuth();
  },
  methods: {
    checkAuth(){
      this.isAuthorized = localStorage.getItem("isAuthorized") ? localStorage.getItem("isAuthorized") : false
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  min-height: 100vh;
}
.main-content{
  padding: 100px 0;
}
</style>
