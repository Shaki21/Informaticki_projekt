<template>
  <div class="random-beer">
    <v-card class="mx-auto my-auto" max-width="400">
        <v-img class="white--text align-center mx-auto" max-width="80" :src="beer.image_url">
        </v-img>
        <v-card-title>{{ beer.name }}</v-card-title>
        <v-card-subtitle>
          {{ beer.id }}
        </v-card-subtitle>

        <v-divider class="mx-4"></v-divider>

        <v-card-text class="text--primary">
          <div>{{ beer.description }}</div>
        </v-card-text>

        <v-divider class="mx-4"></v-divider>
        
        <v-card-text class="text--primary" v-for="food in beer.food_pairing" :key="food">
          {{ food }}
        </v-card-text >

      </v-card>
    <div>

    </div>
  </div>

</template>
<style>
.random-beer {
  height: 100%;
  background-image: url('../assets/piva.jpeg');
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
<script setup>
import axios from "axios";
import { ref } from "vue";

const beer = ref({});

axios.get("https://api.punkapi.com/v2/beers/random").then((res) => {
  beer.value = res.data[0];
});

</script>