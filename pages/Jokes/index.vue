<template>
  <div>
      <SearchJokes v-on:search-text="searchText" />
      <Joke v-for="joke in jokes"
       v-bind:key ="joke.id"
       :id="joke.id"
       :joke="joke.joke"
       />
  </div>
</template>

<script>
import axios from 'axios'
import Joke from '../../components/Joke'
import SearchJokes from '../../components/SearchJokes'

export default {
  components: {
    Joke,
    SearchJokes
  },

  data() {
    return {
      jokes: []
    }
  },
  // using axios
  async created() {
    const config = {
      headers: {
        // return json , can return also webpage with modification
        Accept: 'application/json'
      }
    }
    // calling web site that reurn jokes otherwise return error
    try {
      const res = await axios.get('https://icanhazdadjoke.com/search', config)
      //console.log(res.data.results)
      this.jokes = res.data.results
    } catch (err) {
      console.log(err)
    }
  },
  methods:{
     async searchText(text) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      };
      try {
        const res = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        );
        this.jokes = res.data.results;
      } catch (err) {
        console.log(err);
      }
    }
  },

  head() {
    return {
      title: 'Dad Jokes ',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Best place for Dad jokes'
        }
      ]
    }
  }
}
</script>

<style>
</style>