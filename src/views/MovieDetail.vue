<script setup>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';

const movie = ref({});
const route = useRoute();

onBeforeMount(() => {
  fetch(`https://www.omdbapi.com/?apikey=d466ee26&i=${route.params.id}&plot=full`)
    .then(response => response.json())
    .then(data => {
      movie.value = data
    });
});
</script>



<template>
    <div class="movie-detail">
        <h2>{{movie.Title}}</h2>
        <p>{{movie.Year}}</p>
        <img :src="movie.Poster"/> 
        <p>{{ movie.Plot }}</p>
    </div>
</template>

<style lang="scss">
.movie-detail {
    padding: 16px;
  
    h2 {
      color: #FFF;
      font-size: 28px;
      font-weight: 600;
      margin-bottom: 16px;
    }
  
    .featured-img {
      display: block;
      max-width: 200px;
      margin-bottom: 16px;
    }
  
    p {
      color: #FFF;
      font-size: 18px;
      line-height: 1.4;
    }
  }
</style>

