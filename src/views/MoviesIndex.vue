<template>
  <div class="movies-index">
<!-- 
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
    </div> -->

      <!-- Features -->
    <div id="features-wrapper">
      <div class="container">
        <div class="row">
          <div class="col-4 col-12-medium">

            <!-- Box -->
              <section class="box feature">
                <a href="#" class="image featured"><img src="images/pic01.jpg" alt="" /></a>
                <div class="inner">
                  <header>
                    <h2>Put something here</h2>
                    <p>Maybe here as well I think</p>
                  </header>
                  <p>Phasellus quam turpis, feugiat sit amet in, hendrerit in lectus. Praesent sed semper amet bibendum tristique fringilla.</p>
                </div>
              </section>

          </div>
          <div class="col-4 col-12-medium">

            <!-- Box -->
              <section class="box feature">
                <a href="#" class="image featured"><img src="images/pic02.jpg" alt="" /></a>
                <div class="inner">
                  <header>
                    <h2>An interesting title</h2>
                    <p>This is also an interesting subtitle</p>
                  </header>
                  <p>Phasellus quam turpis, feugiat sit amet in, hendrerit in lectus. Praesent sed semper amet bibendum tristique fringilla.</p>
                </div>
              </section>

          </div>
          <div class="col-4 col-12-medium">

            <!-- Box -->
              <section class="box feature">
                <a href="#" class="image featured"><img src="images/pic03.jpg" alt="" /></a>
                <div class="inner">
                  <header>
                    <h2>Oh, and finally ...</h2>
                    <p>Here's another intriguing subtitle</p>
                  </header>
                  <p>Phasellus quam turpis, feugiat sit amet in, hendrerit in lectus. Praesent sed semper amet bibendum tristique fringilla.</p>
                </div>
              </section>

          </div>
        </div>
      </div>
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