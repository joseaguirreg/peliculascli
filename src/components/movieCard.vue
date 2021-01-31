<template>
  <v-card class="mb-5">
    <v-img
      class="white--text"
      height="180px"
      :src="movie.backdrop_path"
    >
      <v-card-title>{{ movie.title }} </v-card-title>
    </v-img>
    <v-card-text>
      <div class="subtitle-1"> Votos: {{ movie.vote_average }}</div>
      <div class="subtitle-1">Popularidad: {{ movie.popularity }}</div>
      <!-- <div class="subtitle-1">
        Población: {{ populationFormat(country.population) }}
      </div> -->
    </v-card-text>
  </v-card>
</template>

<script>
import Movie from '@/models/movie.js'
export default {
  props: {
    movie: {
      type: Object,
      required: true,
      default: new Movie()
    },
  },
  methods: {
    // populationFormat(population) {
    //   // Expresión regular utilizada para agregar un punto cada 3 números
    //   return population.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
    // },
  },
};
</script>

<style>
</style>