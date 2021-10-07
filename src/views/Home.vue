<template>
  <div class="home">
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <router-link :to="'/movie/' + movie.id" class="movie-link">
          <h3>{{movie.fullTitle}}</h3>
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
    h3{
      color: #000000;
      font-size: 0.875rem;
      font-weight: 400;
      font-family: 'Lucida Sans', sans-serif;
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
