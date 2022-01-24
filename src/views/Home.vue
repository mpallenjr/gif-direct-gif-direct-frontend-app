<template>
  <div class="home">
    <h1>Search for GIF</h1>
    <p> 
      <input type="text" v-model="searchCriteria.keywords">
      <button v-on:click="searchGIF()"> Search </button> 
    </p> 
      {{searchedGIFS}}
    <h1> Translate to GIF </h1>
    <p> 
      <input type="text" v-model="searchCriteria.translate">
      <button v-on:click="translateGIF()"> Translate </button>
    </p>
      {{translatedGIFS}}
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
        trendingGIFS: [],
        searchCriteria: [],
        searchedGIFS: [],
        translatedGIFS: []
      };
    },
    created: function () {
      axios.get("http://localhost:3000/trending_gifs").then(response => {
          console.log(response.data)
          this.trendingGIFS = response.data
      }
      )
    },
    methods: {
      translateGIF: function () {
        console.log(this.searchCriteria.translate);
        axios.get(`http://localhost:3000/translate_gifs?translate=${this.searchCriteria.translate}`).then(response => {
        this.translatedGIFS = response.data
        })
      },
      searchGIF: function () {
      axios.get(`http://localhost:3000/searched_gifs?keywords=${this.searchCriteria.keywords}`).then(response => {
          this.searchedGIFS = response.data
        })
      }
    },
  };
</script>
