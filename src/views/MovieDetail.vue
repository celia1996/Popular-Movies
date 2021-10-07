<template>
  <div class="movie-detail">
    <div class="movie-description">
    <h1>{{movie.title}}</h1>
    <img :src="movie.image" alt="Movie Poster" class="featured-img" />
      <h2>Movie details</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Director: {{ movie.directors }}</p>
      <p>Release date: {{ movie.releaseDate }}</p>
      <p>Genres: {{ movie.genres }}</p>
      <p>Plot: {{ movie.plot }}</p>
    </div>
    <div class="cast">
    <h2>Cast</h2>
      <div class="actor" v-for="actor in movie.actorList" :key="actor.id">
        <p>{{ actor.name }} as {{actor.asCharacter}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';
export default {
  setup () {
    const movie = ref({});
    const route = useRoute();
    onBeforeMount(() => {
      fetch(`https://imdb-api.com/en/API/Title/${env.apikey}/${route.params.id}`)
        .then(response => response.json())
        .then(data => {
          console.log(data)
          movie.value = data;
        });
    });
    return {
      movie
    }
  }
}
</script>

<style lang="scss">
.movie-detail {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  align-items: center;
  .movie-description{
    width: 40rem ;
  }
  p{
    padding: 0.5rem;
    max-width: 40rem;
    font-size: 0.875rem;
    font-weight: 400;
  }
  h1 {
    font-size: 2.5rem;
    font-weight: 200;
    margin-bottom: 1rem;
  }
  h2 {
    margin-bottom: 1rem;
  }
  .featured-img {
    display: block;
    max-width: 15rem;
    margin-bottom: 1rem;
  }
  .cast {
    display: flex;
    flex-wrap: wrap;
    flex-direction: column;
    align-self: center;
    width: 40rem;
    margin-top: 1rem;
  }
}
</style>