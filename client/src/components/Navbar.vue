<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark rounded">
    <button class="navbar-toggler"
    type="button"
    data-toggler="collapse"
    data-target="#navbar1"
    aria-controls="navbar1"
    aria-expand="false"
    aria-label="Toggle Navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse justify-content-md-center" id="navbar1">
    <ul class="navbar-nav">
      <li class="nav-item">
        <router-link class="nav-link" to="/">Home</router-link>
      </li>
      <li v-if="auth==''" class="nav-item">
        <router-link class="nav-link" to="/login">Login</router-link>
      </li>
      <li v-if="auth==''" class="nav-item">
        <router-link class="nav-link" to="/register">Register</router-link>
      </li>
      <li v-if="auth=='loggedin'" class="nav-item">
        <router-link class="nav-link" to="/profile">Profile</router-link>
      </li>
      <li v-if="auth=='loggedin'" class="nav-item">
        <a class="nav-link" href="" v-on:click="logout">Logout</a>
      </li>
    </ul>
  </div>
</nav>
</template>

<script>
import EventBus from './EventBus'
export default {
  data () {
    return {
      auth: '',
      user: ''
    }
  },

  methods: {
    logout () {
      localStorage.removeItem('usertoken')
    }
  },

  mounted () {
    EventBus.$on('logged-in', status => {
      this.auth = status
    })
  }
}
</script>
