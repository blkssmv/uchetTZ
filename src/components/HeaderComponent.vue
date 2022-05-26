<template>
  <header class="header">
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <div class="container">
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
        <b-collapse class="justify-content-between" id="nav-collapse" is-nav>
          <b-navbar-nav>
            <b-nav-item>Home</b-nav-item>
            <b-nav-item>About us</b-nav-item>
            <b-nav-item>Help</b-nav-item>
            <b-nav-item>Contacts</b-nav-item>
          </b-navbar-nav>
          <b-navbar-nav class="ml-auto">
            <b-nav-item href="/" @click="logout">Log out</b-nav-item>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </header>
</template>

<script>
import Vue from 'vue'
import {BootstrapVue} from 'bootstrap-vue'

import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

Vue.use(BootstrapVue)

export default {
  methods: {
    logout(){
      localStorage.clear()
    }
  }
}
</script>

<style scoped>
.header {
  position: fixed;
  width: 100%;
  z-index: 1000;
}
</style>