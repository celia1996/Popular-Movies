<template>
  <div class="home">
    <div class="movies-list">
    <div v-for="movie in movies"
    :key="movie.id">
      <h3>{{movie.fullTitle}}</h3>
      <img :src="movie.image" alt="Movie Poster"/>
    </div>
    </div>
  </div>
</template>

<script>

import { ref, onBeforeMount } from 'vue';
import env from '@/env.js'
export default {
  setup () {
    const movies = ref([]);
    onBeforeMount(() => {
        fetch(`https://imdb-api.com/en/API/MostPopularMovies/${env.apikey}`)
          .then(response => response.json())
          .then(data => {
            console.log(data)
            movies.value = data.items;
        })
    })
    return {
      movies
    }
  }
}
</script>

<style lang="scss">
.movies-list {
    flex-wrap: wrap;
    display: flex;
}
</style>
