<template>
  <div class="all-beers">
    <div class="d-flex flex-column">
      <div class="d-flex justify-center">
        <span class="text-h4 font-weight-medium  mt-3">Sve pive</span>
      </div>
      <div class="d-flex justify-center">
        <v-text-field label="Unesite naziv proizvoda..." prepend-inner-icon="mdi-magnify" clearable v-model="input"  style="max-width: 380px"></v-text-field>
      </div>
    </div>
    <v-row>
      <v-col class="justify-center align-center" v-for="beer in filteredList()" cols="12" xl="3" md="4" :key="beer">
        <v-card class="mx-auto my-auto">
          <v-img class="white--text align-center mx-auto" max-width="80" :src="beer.image_url"> </v-img>
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
import { ref } from "vue";
import axios from "axios";

const beers = ref([]);

axios.get("https://api.punkapi.com/v2/beers").then((res) => {
  beers.value = res.data;
  console.log(res.data);
});

let input = ref("");
function filteredList() {
  return beers.value.filter((beer) => beer.name.toLowerCase().includes(input.value.toLowerCase()));
}
</script>
