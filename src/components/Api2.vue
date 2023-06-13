<template>
    <div>
        <div>
            <select v-model="selectedMovie" class="form-select" aria-label="Default select example" @change="fetchMovieDetails">
        <option value="" disabled selected>Seleccione una película</option>
        <option v-for="movie in movies" :key="movie.id" :value="movie">{{ movie.title }}</option>
      </select>
    </div>
    <div v-if="selectedMovie">
      <div class="card" style="width: 18rem;">
        <img :src="selectedMovie.poster" class="card-img-top" alt="...">
        <div class="card-body">
          <h5 class="card-title">{{ selectedMovie.title }}</h5>
          <p class="card-text">{{ selectedMovie.description }}</p>
        </div>
        <ul class="list-group list-group-flush">
          <li class="list-group-item">Director: {{ selectedMovie.director }}</li>
          <li class="list-group-item">Duración: {{ selectedMovie.runtimeMinutes }} minutos</li>
        </ul>
        <div class="card-body">
          <a href="#" class="card-link">Card link</a>
          <a href="#" class="card-link">Another link</a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'component-name',
  data() {
    return {
      movies: [],
      selectedMovie: null,
    };
  },
  methods: {
    fetchMovies() {
      axios.get('https://studio-ghibli-films-api.herokuapp.com/api')
        .then(response => {
          this.movies = response.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    fetchMovieDetails() {
      const selectedMovieId = this.selectedMovie.id;
      this.selectedMovie = this.movies.find(movie => movie.id === selectedMovieId);
    },
  },
  mounted() {
    this.fetchMovies();
  },
};
</script>

<style scoped>
</style>
