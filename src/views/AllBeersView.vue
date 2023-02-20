<template>
  <div class="all-beers">
    <div class="d-flex flex-column">
      <div class="d-flex justify-center">
        <span class="text-h4 font-weight-medium mt-3">All Beers</span>
      </div>
      <div class="d-flex justify-center">
        <v-text-field label="Unesite naziv proizvoda..." prepend-inner-icon="mdi-magnify" clearable v-model="input" style="max-width: 380px" @input="search()"></v-text-field>
      </div>
    </div>
    <v-row>
      <v-col class="justify-center align-center" v-for="beer in items" cols="12" xl="3" lg="4" md="6" :key="beer.id">
        <v-card class="mx-auto my-auto">
          <v-img class="white--text align-center mx-auto" max-width="100" :src="beer.image_url"> </v-img>
          <v-card-title>{{ beer.name }}</v-card-title>
          <v-card-subtitle>
            {{ beer.id }}
          </v-card-subtitle>
          <v-divider class="mx-4"></v-divider>
          <v-card-text class="text--primary">
            <div>{{ beer.description }}</div>
          </v-card-text>
          <v-divider class="mx-4"></v-divider>
          <v-card-text class="text--primary">
            <div>{{ beer.food_pairing[0] }}</div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-pagination v-model="page" :length="Math.ceil(paginatedBeers.length / perPage)"></v-pagination>
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
  background-image: url("../assets/13.jpeg");
  background-size: cover;
}
</style>
<script setup>
import { ref, computed } from "vue";
import axios from "axios";

const beers = ref([]);
const paginatedBeers = ref([]);
let input = ref("");
const page = ref(1);
const perPage = ref(8);

// Search
function search() {
  paginatedBeers.value = beers.value.filter((beer) => beer.name.toLowerCase().includes(input.value.toLowerCase()));
}
// Pagination
const items = computed(() => {
  return paginatedBeers.value.slice((page.value - 1) * perPage.value, page.value * perPage.value);
});

axios.get("https://api.punkapi.com/v2/beers").then((res) => {
  beers.value = res.data;
  paginatedBeers.value = res.data;
  console.log(res.data);
});
</script>
