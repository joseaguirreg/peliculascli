<template>
  <v-container>
    <h1>Nombre: {{movie.title }}</h1>
    <Loader :isLoading="isLoading" />
    <movieCard v-if="!isLoading" :movie="movie" />
  </v-container>
</template>

<script>
import apiService from "@/services/api.service";
import Movie from "@/models/movie.js";
export default {
  data() {
    return {
      movie: [],
      isLoading: true,
    };
  },
  created() {
    this.getMovie2();
  },
  methods: {
    getMovie2() {
      apiService
        .getMovie(this.$route.params.id).then(({data}) => {
          this.isLoading = false;
          this.movie = new Movie(data);
          // this.movie = response.data[0];
          console.log(this.$route.params.id);
        })
        .catch((error) => {
          this.isLoading = false;
          alert(error);
        });
    },
  },
};
</script>

<style>
</style>