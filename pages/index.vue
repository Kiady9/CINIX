<template>
  <div>
      <div class="row">
        <h2>Les plus <strong>Populaires</strong></h2>
      </div>
    
    
     <vueper-slides
      ref="vueperslides1"
      @slide="$refs.vueperslides2 && $refs.vueperslides2.goToSlide($event.currentSlide.index, { emit: false })"
      :slide-ratio="1 / 4"
      :bullets="false">
  
  <vueper-slide
      v-for="(movie, index) in movies.results"
      :key="index"
      :title=" movie.original_title.toString()"
      content="Navigation in sync"
      :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2'+movie.poster_path" />
</vueper-slides>

<vueper-slides
      ref="vueperslides2"
      :slide-ratio="1 / 8"
      :dragging-distance="50"
      @slide="$refs.vueperslides1 && $refs.vueperslides1.goToSlide($event.currentSlide.index, { emit: false })"
      :visible-slides="3"
      fixed-height="100px">
  <vueper-slide
      v-for="(movie, index) in movies.results "
      :key="index"
      @click.native="$refs.vueperslides2 && $refs.vueperslides2.goToSlide(i - 1)">
    
    <template #content>
      <div class="vueperslide__content-wrapper" :style="'background-color: ' + ['#ff5252', '#42b983'][i % 2]">
        <div class="vueperslide__title">{{  movie.original_title.toString() }}</div>
      </div>
    </template>
    
  </vueper-slide>
</vueper-slides>

  <div class="row">
        <h2><strong>Nouveaux Films</strong></h2>
      </div>
    <div class="container">
      
      <vueper-slides
        class="no-shadow"
        :visible-slides="4"
        slide-multiple
        :gap="3"
        :slide-ratio="1 / 4"
        :dragging-distance="200"
        :breakpoints="{ 800: { visibleSlides: 2, slideMultiple: 2 } }"
        :arrowsOutside="false">

        <vueper-slide 
          v-for="(movie, index) in movies.results" 
          :key="index" 
          :title=" movie.original_title .toString()" 
          :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2'+movie.poster_path" />
      
      </vueper-slides>
    </div>
  </div>
  
</template>

<script>   
import { VueperSlides, VueperSlide } from 'vueperslides'
import 'vueperslides/dist/vueperslides.css'

export default {
   components: { VueperSlides, VueperSlide },
  async asyncData({ $http }) {
    const movies = await $http.$get(
      "https://api.themoviedb.org/3/movie/now_playing?api_key=031527da0c50b6f502203e476ecc877f"
    );
    return { movies };
      console.log(movies);
  },

};


</script>

<style>
  *{
    margin: 0;
    padding: 0;
  }

  body{
    background-color: #09062F;
  }

  .container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    height: auto;
    width: 100vw;
    
  } 
  .row{
    justify-content:center;
    color: #fff;
    display: flex;
    margin-top: 20px;
  }

  .vueperslides {
    width: 100%;
  }

  .vueperslide__title {
      width: 100%;
      background-color: rgba(0, 0, 0, 0.5);
      padding: 4px 0;
      color: #fff;
  }

  .vueperslides__bullet{
      margin: 1.5em .6em;
      padding: 0;
      border-radius: 100%;
      background-color: #fff ;
  }

  .vueperslides__arrows {
    font-size: 10px;
    color: #fff !important;
  }
</style>