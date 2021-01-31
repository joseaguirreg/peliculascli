<template>
  <v-container>
    <v-layout md12>
      <v-text-field
        v-model="search"
        append-icon="mdi-search"
        placeholder="Buscar"
        single-line
      />
    </v-layout>
    <Loader :isLoading="isLoading" />
    <v-layout wrap md12>
      <v-flex
        v-for="(movie, index) in moviesFilter"
        :key="index"
        :search="search"
        @click="openMovie(movie.id)"
        md3
        sm4
        xs12
        px-2
      >
        <movieCard :movie="movie" />
      </v-flex>
    </v-layout>
    <v-btn @click="getMovies()">Ver más</v-btn>
  </v-container>
</template>

<script>
import ApiService from "@/services/api.service";
import Movie from '@/models/movie.js';
export default {
  data() {
    return {
      movies: [],
      search: "",
      isLoading: true,
    };
  },
  created() {
    setTimeout(() => {
      this.getMovies();
    }, 500);
  },
  computed: {
    moviesFilter() {
      return this.movies.filter((e) => {
        return e.title.toLowerCase().indexOf(this.search.toLowerCase()) !== -1;
      });
    },
  },
  methods: {
    getMovies() {
      ApiService
        .getTopRated()
        .then((response) => {
          this.isLoading = false;
          // this.countries = response.data;
          
          console.log(response.data);
          this.movies = response.data.results.map(movie => new Movie(movie));
          console.log(this.movies);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    openMovie(id) {
      // this.$router.push(`/countries/${name}`);
      this.$router.push({ path: `/movies/${id}` })
      // this.$router.push({ title: 'Movie', params: {  title } })
      // .catch(()=>{})
      
    }
  },
};
</script>