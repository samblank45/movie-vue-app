<template>
   <div class="movies-show">
      <h2> {{ movie.title }} </h2>
      <p> {{ movie.year }} </p>
      <p> {{ movie.plot }} </p>
      <p> {{ movie.director }} </p>
      <p> {{ movie.english }} </p>
      <router-link :to="`/movies/${movie.id}/edit`"> Edit </router-link>
    <button v-on:click="destroyMovie()">DELETE</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      this.movie = response.data;
      console.log(response.data);
    });
  },
  methods: {
    destroyMovie: function() {
      if (confirm("are you sure you want to delethis this?")) {
        axios.delete(`/api/movies/${this.movie.id}`).then(response => {
          console.log("successfully destroyed", response.data);
          this.$router.push("/movies");
        });
      }
    }
  }
};
</script>