<template>
  <div class="movies-index">

    <div> search: <input type="text" v-model="titleFilter" list='titles' /> </div>
    <datalist id="titles">
      <option v-for="movie in movies"> {{movie.title}}</option>
    </datalist>
    <div>
      <button> Sort Alphabetically</button>
    </div>
    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')">
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
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      titleFilter: ""
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