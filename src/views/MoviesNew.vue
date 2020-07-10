
<template>
  <div class="movies-new">

    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
       <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>title:</label>
        <input type="text" class="form-control" v-model="title">
      </div>
      <div class="form-group">
        <label>plot:</label> <br>
        <small class="text-success" v-if="plot.length <= 50"> Characters remaining: {{50 - plot.length}}</small>
        <small class="text-danger" v-if="plot.length > 50"> Exceeded character limit.</small>
        <input type="text" class="form-control" v-model="plot">
      </div>
      <div class="form-group">
        <label> year:</label>
        <input type="text" class="form-control" v-model="year">
      </div>
      <div class="form-group">
        <label> director:</label>
        <input type="text" class="form-control" v-model="director">
      </div>
       <div class="form-group">
        <label> english:</label>
        <input type="text" class="form-control" v-model="english">
      </div>
      <input type="submit" class="btn btn-primary" value="create">
    </form>

  </div>
</template>


<script>
import axios from "axios";
export default {
  data: function() {
    return {
      errors: [],
      title: "",
      plot: "",
      year: "",
      director: "",
      english: ""
    };
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.title,
        plot: this.body,
        year: this.year,
        director: this.director,
        english: this.english
      };
      axios
        .post("/api/movies", params)
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
