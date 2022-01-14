<template>
  <div>
    <div>
      <p>Ici on met la bar de navigation et la page d'audessus</p>
    </div>
    <div>
      <h2>Les plus POPULAIRES</h2>
      <vueper-slides
        class="no-shadow"
        :visible-slides="2"
        slide-multiple
        :gap="3"
        :slide-ratio="1 / 4"
        :dragging-distance="200"
        :breakpoints="{ 800: { visibleSlides: 2, slideMultiple: 2 } }"
        :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2/'+movies.poster_path" 
      >
      <vueper-slide 
        v-for="(movie, i) in movies.results" 
        :key="i" 
        :title=" movie.original_title .toString()" 
        :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2'+movie.poster_path" />
      </vueper-slides>
    </div>
    <div>
      <h2 class="titre-vueperslide">LES PLUS RECENTS</h2>
      <vueper-slides style="margin-top 25px;"
        class="no-shadow"
        :visible-slides="4"
        slide-multiple
        :gap="2"
        :bullets="false"
        :slide-ratio="1 / 2"
        :dragging-distance="200"
        :breakpoints="{ 800: { visibleSlides: 2, slideMultiple: 2 } }"
        :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2/'+movies.poster_path"
         
      >
      <vueper-slide 
            v-for="(movie, i) in movies.results" 
            :key="i" 
            :title=" movie.original_title .toString()" 
            :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2'+movie.poster_path" />
      </vueper-slides>
    </div>
    <div>
      <h2>HORREUR</h2>
      <vueper-slides
        class="no-shadow"
        :visible-slides="4"
        slide-multiple
        :gap="3"
        :slideContentOutside="true"
        :bullets="false"
        :slide-ratio="1 / 4"
        :dragging-distance="200"
        :breakpoints="{ 800: { visibleSlides: 2, slideMultiple: 2 } }"
        :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2/'+movies.poster_path"
         
      >
      <vueper-slide 
        v-for="(movie, i) in movies.results" 
        :key="i" 
        :title=" movie.original_title .toString()" 
        :image="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2'+movie.poster_path" />
      </vueper-slides>
    </div>
    <div>
      <p>Apres je pense sa sera la suite de la page dpnc je sais pas trop</p>
    </div>
  </div>

  <!-- <div> -->
    <!-- <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else> -->
    <!-- <div class="container-fluid h-100 d-inline-block">
      <h1>Search</h1> -->
      <!-- <button @click="getDataDrinks()">SHOW DRINKS</button>
      <input v-model="search" /> -->
      <!-- <div v-for="(movie, index) in movies.results" :key="index" class="row">
        <div class="card" style="width: 18rem">
          <img
            class="card-img-top"
            :src="'https://www.themoviedb.org/t/p/w600_and_h900_bestv2/'+movie.poster_path"
            alt="Card image cap"
          /> 
          <div class="card-body">
            <h5 class="card-title">{{ movie.original_title }}</h5> -->
                        <!-- <p class="card-text">
              {{ drink.strCategory }}
            </p> -->
            <!-- <p class="card-text">
              {{ drink.strInstructions }}
            </p>
            <a :id="drink.idDrink" href="#" class="btn btn-primary">DETAILS</a> -->
            
          <!-- </div>
          
        </div>
      </div>
    </div> -->
    <!-- <div id="carouselExampleControls" class="carousel slide" data-ride="carousel">
    <div class="carousel-inner">
        <div class="carousel-item active">
        <img class="d-block w-100" src="..." alt="First slide">
        </div>
        <div class="carousel-item">
        <img class="d-block w-100" src="..." alt="Second slide">
        </div>
        <div class="carousel-item">
        <img class="d-block w-100" src="..." alt="Third slide">
        </div>
    </div>
    <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-slide="prev">
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="sr-only">Previous</span>
    </a>
    <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-slide="next">
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="sr-only">Next</span>
    </a>
    </div> -->
  <!-- </div> -->
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

          //On creer une function getdatadrink pour quand on click on recupere l'api
// export default {
//   name: "cp",
//   data() {
//     return {
//       drinks: {},
//     };
//   },
//   methods: {
//     // test(event) {
//     //   // now we have access to the native event
//     //   if (event) {
//     //     event.preventDefault();
//     //   }
//     //   alert("click");
//     // },
//     getDataDrinks: function () {
//       fetch(
//         "https://api.themoviedb.org/3/movie/now_playing?api_key=031527da0c50b6f502203e476ecc877f" +
//           this.search
//       )
//         .then((response) => response.json())
//         .then((data) => (this.drinks = data.drinks));
//     },
//   },
  //   async fetch() {
  //     this.drinks = await fetch(
  //       "https://www.thecocktaildb.com/api/json/v1/1/search.php?f=a"
  //     ).then((res) => res.json());
  //   },
// };
</script>      

<style>
    #__layout{
      background-color: #09062F;
      color: white;
      padding: 10px;
    }

    .vueperslides{
      margin: 25px;
    }

    .vueperslide{
      background-repeat: no-repeat;
      border-radius: 21px;
    }

    .vueperslide__title{
        color: white;
        width: 100%;
       
        
    }

    

    .vueperslide__content-wrapper {
        
      display: flex-end !important;
    }
</style>