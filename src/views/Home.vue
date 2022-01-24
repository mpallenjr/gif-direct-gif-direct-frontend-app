<template>
  <div class="home">
    <h1>Search for GIF</h1>
   <p> <input type="text">
    <button> Search </button> </p> 

<h1> Translate to GIF </h1>
   <p> <input type="text">
    <button> Translate </button></p>
<h1> Trending GIFS </h1>
  <div v-for="data in trendingGIFS">
    <div v-for="gif in data">
      <iframe v-bind:src="gif.embed_url" width="20%" height="20%" style="border:1px solid black;">
      </iframe>
      <br/>
      <br/>
      </div>
  </div>

  </div>
</template>

<style></style>

<script>
import axios from 'axios';
  export default {
    data: function () {
      return {
        message: "Welcome to Vue.js!",
        trendingGIFS: []
      };
    },
    created: function () {
      axios.get("http://localhost:3000/trending_gifs").then(response => {
          console.log(response.data)
          this.trendingGIFS = response.data
      }
      )
    },
    methods: {},
  };
</script>}
