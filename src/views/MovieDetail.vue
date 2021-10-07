<template>
  <div class="movie-detail">
    <div class="movie-description">
    <h1>{{movie.title}}</h1>
    <img :src="movie.image" alt="Movie Poster" class="featured-img" />
    <h2>Movie details</h2>
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.directors }}</p>
    <p>Release date: {{ movie.releaseDate }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <p>Genres: {{ movie.genres }}</p>
    </div>
    <h2>Cast</h2>
    <div class="cast">
      <div class="actor" v-for="actor in movie.actorList" :key="actor.id">
        <img :src="actor.image" alt="Actor photo" class="actor-img" />
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
    margin-bottom: 1rem;
  }
  p{
    padding: 0.5rem;
  }
  h1 {
    font-size: 2.5rem;
    font-weight: 200;
    margin-bottom: 16px;
  }
  .featured-img {
    display: block;
    max-width: 15rem;
    margin-bottom: 1rem;
  }
  .cast{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    .actor-img {
      position: relative;
      width: 200px;
      height: 200px;
      overflow: hidden;
      border-radius: 50%;
  }
  .actor {
    padding: 1rem;
    margin: 1rem;
}
  }
}
</style>