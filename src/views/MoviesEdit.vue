
<template>
  <div class="movies-new">

    <form v-on:submit.prevent="editMovie()">
      <h1>Update Movie</h1>
       <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>title:</label>
        <input type="text" class="form-control" v-model="movie.title">
      </div>
      <div class="form-group">
        <label>plot:</label>
        <input type="text" class="form-control" v-model="movie.plot">
      </div>
      <div class="form-group">
        <label> year:</label>
        <input type="text" class="form-control" v-model="movie.year">
      </div>
      <div class="form-group">
        <label> director:</label>
        <input type="text" class="form-control" v-model="movie.director">
      </div>
       <div class="form-group">
        <label> english:</label>
        <input type="text" class="form-control" v-model="movie.english">
      </div>
      <input type="submit" class="btn btn-primary" value="update">
    </form>

  </div>
</template>


<script>
import axios from "axios";
export default {
  data: function() {
    return {
      errors: [],
      movie: {}
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
      this.movie = response.data;
      console.log(this.movie);
    });
  },
  methods: {
    editMovie: function() {
      var params = {
        title: this.movie.title,
        plot: this.movie.plot,
        year: this.movie.year,
        director: this.movie.director,
        english: this.movie.english
      };
      axios
        .patch(`/api/movies/${this.movie.id}`, params)
        .then(response => {
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch(error => {
          this.error = error.response.data.errors;
        });
    }
  }
};
</script>
