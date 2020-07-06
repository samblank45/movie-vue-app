<template>
   <div class="home">
     <h1> New Movie </h1>
     <div>
        Title: <input type="text" v-model="newMovieTitle"> <br>
        Plot: <input type="text" v-model="newMoviePlot"> <br>
        year: <input type="text" v-model="newMovieYear"> <br>
        director: <input type="text" v-model="newMovieDirector"> <br>
        <button v-on:click="createMovie()"> Create </button>
     </div>

     <div v-for="movie in movies">
       <h1> {{movie.title}} </h1>
       <h3> Director: {{movie.director}} </h3>
       <h3> Release Date: {{movie.year}} </h3>
       <h3> Plot: {{movie.plot}} </h3>
       <button v-on:click="showMovie(movie)">More Info </button>
     </div>

     <dialog id="movie-details">
       <form method="dialog">
         <h1> Movie Info </h1>
         <p> Title: <input type="text" v-model="currentMovie.title"></p>
         <p> Plot: <input type="text" v-model="currentMovie.plot"></p>
         <p> Year: <input type="text" v-model="currentMovie.year"></p>
         <p> Director: <input type="text" v-model="currentMovie.director"></p>
         <button> close </button>
         <button v-on:click="updateMovie(currentMovie)">Update</button>
         <button v-on:click="destroyMovie(currentMovie)">Delete</button>
       </form>
     </dialog>
  </div>
  
</template>

<style>
h1 {
  color: rgb(21, 100, 39);
}
h3 {
  color: rgb(116, 116, 196);
}
body {
  background-color: blanchedalmond;
}
.add {
  color: rgb(134, 26, 26);
}
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      currentMovie: {}
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log("all movies :", response.data);
        this.movies = response.data;
      });
    },
    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector
      };
      axios.post("/api/movies", params).then(response => {
        console.log("success", response.data);
        this.movies.push(response.data);
      });
    },
    showMovie: function(movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director
      };
      axios
        .patch(`/api/movies/${movie.id}`, params)
        .then(response => {
          console.log("successfully updated", response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
    destroyMovie: function(movie) {
      axios.delete(`/api/movies/${movie.id}`).then(response => {
        console.log("successfully destroyed", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    }
  }
};
</script>