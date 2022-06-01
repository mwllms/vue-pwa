<script setup>
import { reactive, ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import ReloadPWA from './components/ReloadPWA.vue'
import axios from 'axios'

const isAuthenticated = ref(false)
const form = reactive({
  username: '',
  password: '',
})

const login = async () => {
  try {
    const response = await axios.post('https://marketingapi.nl/auth/login', form)
    isAuthenticated.value = true
  } catch (error) {
    isAuthenticated.value = false
    console.log(error)
  }
}
</script>

<template>
  <ReloadPWA />
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3 + Vite" />
  <div>
    <form @submit.prevent="login">
      <div>
        <label for="email">Email</label>
        <input type="email" id="email" v-model="form.username" />
      </div>
      <div>
        <label for="password">Password</label>
        <input type="password" id="password" v-model="form.password" />
      </div>
      <button type="submit">Login</button>
    </form>
    <div>
      {{ isAuthenticated }}
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
