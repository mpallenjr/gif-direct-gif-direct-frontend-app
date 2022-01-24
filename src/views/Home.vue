<template>
  <div class="home">
    <h1>Search for GIF</h1>
    <p> 
      <input type="text" v-model="searchCriteria.keywords">
      <button v-on:click="searchGIF()"> Search </button> 
    </p> 
    <div v-for="gif in searchedGIFS.data">
      <iframe v-bind:src="gif.embed_url" width="20%" height="20%" style="border:1px solid black;">
      </iframe>
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
        searchCriteria: [],
        searchedGIFS: []
    };
    },
    created: {

    },
    methods: {
      searchGIF: function () {
      axios.get(`http://localhost:3000/searched_gifs?keywords=${this.searchCriteria.keywords}`).then(response => {
          this.searchedGIFS = response.data
        })
      }
    },
  };
</script>
