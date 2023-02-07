<template>
  <div class="all-beers">
    <v-row>
      <v-col class="justify-center align-center" v-for="beer in beers" cols="12" xl="3" :key="beer.id">
        <v-card class="mx-auto my-auto">
        <v-img class="white--text align-end" height="200px" :src="beer.image_url">
          <v-card-title>{{ beer.name }}</v-card-title>
        </v-img>
        <v-card-subtitle>
          {{ beer.id }}
        </v-card-subtitle>

        <v-divider class="mx-4"></v-divider>

        <v-card-text class="text--primary">
          <div>{{ beer.description }}</div>
        </v-card-text>

        <v-divider class="mx-4"></v-divider>

        <v-card-text class="text--primary">
          <div> {{ beer.food_pairing[0] }} </div>
        </v-card-text>
      </v-card>
      </v-col>
    </v-row>
  </div>
</template>
<style> 
  .v-card {
    height: 100%;
    width: 400px;
    padding: 10px;
    margin-top: 15px;
  }
  .all-beers {
  background-image: url('../assets/13.jpeg');
  background-size: cover;
  }

</style>
<script setup>

import { ref } from 'vue';
import axios from 'axios';

const beers = ref([]);

axios.get('https://api.punkapi.com/v2/beers')
  .then(res => {
    beers.value = res.data;
    console.log(res.data);
  })
</script>
