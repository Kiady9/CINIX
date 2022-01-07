<template>

  <div>

    <!-- <p v-if="$fetchState.pending">Fetching mountains...</p>
    <p v-else-if="$fetchState.error">An error occurred :(</p>
    <div v-else> -->
    <div class="container-fluid h-100 d-inline-block">
      <h1>Search</h1>
      <!-- <button @click="getDataDrinks()">SHOW DRINKS</button>
      <input v-model="search" /> -->
      <div v-for="(movie, index) in movies" :key="index" class="row">
        <div class="card" style="width: 18rem">
          <!-- <img
            class="card-img-top"
            :src="production_compagnies.logo_path"
            alt="Card image cap"
          /> -->
          <div class="card-body">
            <h5 class="card-title">{{ movie.original_title }}</h5>
                        <!-- <p class="card-text">
              {{ drink.strCategory }}
            </p> -->
            <!-- <p class="card-text">
              {{ drink.strInstructions }}
            </p>
            <a :id="drink.idDrink" href="#" class="btn btn-primary">DETAILS</a> -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  async asyncData({ $http }) {
    const movies = await $http.$get(
      "https://api.themoviedb.org/3/movie/now_playing?api_key=031527da0c50b6f502203e476ecc877f"
    );
    return { movies };
  },
};
</script>