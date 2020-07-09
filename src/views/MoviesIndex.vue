<template>
  <div class="movies-index">

    <div v-for="movie in movies">
      <h1> {{ movie.title }} </h1>
      <h3> {{movie.plot }} </h3>
      <h3> {{movie.year }} </h3>
      <h3> {{movie.director }} </h3>
      <router-link v-bind:to="`/movies/${movie.id}`"> More info </router-link>
    </div>

  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: []
    };
  },
  created: function() {
    axios.get("/api/movies").then(response => {
      console.log("all movies", response.data);
      this.movies = response.data;
    });
  },
  methods: {}
};
</script>