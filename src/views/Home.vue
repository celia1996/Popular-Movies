<template>
  <div class="home">
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <router-link :to="'/movie/' + movie.id" class="movie-link">
          <h2>{{movie.fullTitle}}</h2>
          <div class="image">
          <img :src="movie.image" alt="Movie Poster"/>
          </div>
        </router-link>
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
    padding: 1rem;
    justify-content: center;
}
.movie{
  width: 15rem;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  .movie-link {
    display: flex;
    flex-direction: column;
    height: 100%;
    h2{
      color: #000000;
      font-size: 1rem;
      font-weight: 700;
      padding: 0.5rem;
    }
    .image {
      display: block;
      width: 100%;
      height: 18rem;
      object-fit: cover;
    img{
      padding: 0.5rem;
    }
    }
  }
}
</style>
