<template>
  <div>
    <h3>ID: {{$route.params.id}}</h3>
    
    <h2>{{joke}}</h2>
    <hr />
    <nuxt-link to="/jokes">Back To Jokes</nuxt-link>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      joke: {}
    }
  },
  head() {
    return {
      title: 'Joke',
      meta: [
        {
          hid: 'joke',
          name: 'joke',
          content: 'Best place for Dad jokes'
        }
      ]
    }
  },
  async created() {
    const config = {
      headers: {
        // return json , can return also webpage with modification
        Accept: 'application/json'
      }
    }
    // calling web site that reurn jokes otherwise return error
    try {
      const res = await axios.get(
        `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
        config
      )
      //console.log(res.data.results)
      this.joke = res.data.joke
    } catch (err) {
      console.log(err)
    }
  }
}
</script>

<style>
</style>