<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">
        nuxt-introduction
      </h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
    <div>
      <!-- {{ users[0].id }}, {{ users[0].name }} -->
      <ul>
        <li v-for="user in users" :key="user.id">
          {{ user.id }}, {{ user.name }}, {{ user.company.name }}
        </li>
      </ul>
    </div>

    <div>
      <img src="~/assets/cat.jpg">
    </div>

    <div>
      <!-- <p>{{ $store.state.message }}</p> -->
      <!-- <p>{{ $store.state.hello.message }}</p> -->
      <p>{{ $store.state.hello.message }}</p>

      <!-- <button v-on:click="$store.commit('updateMessage')">Update</button> -->
      <!-- <button v-on:click="$store.commit('updateMessage', 'Commit with payload')">Update</button> -->
      <!-- <button v-on:click="$store.dispatch('updateMessageAction')">Dispatch</button> -->
      <!-- <button v-on:click="$store.dispatch('updateMessageAction', 'Dispatch with payload')">Dispatch</button> -->
      <!-- <button v-on:click="$store.dispatch('hello/updateMessageAction', 'Dispatch with payload')">Dispatch</button> -->
      <button v-on:click="$store.dispatch('hello/updateMessageAction', 'Dispatch with payload')">Dispatch</button>

    </div>

    <div>
      <Counter></Counter>
      <hr>
      <Counter></Counter>
      <hr>
      <Counter></Counter>
      <hr>
    </div>
  </div>
</template>

<script>
import Counter from '~/components/Counter.vue'

const axios = require('axios')
let url = 'https://jsonplaceholder.typicode.com/users'

export default {
  //asyncDataはnuxtのメソッド
  asyncData({ params, error }) {
    return axios.get(url)
    .then((res => {
      return {users: res.data}
    }))
    .catch(( e => {
      console.log(e.response.status)
      console.log(error)
      // error({ users: e.response.status, message: 'Error!'})
    }))
  },
  components: {
    Counter
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  /* font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif; */
  font-family: 'Permanent Marker', cursive;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
