import type { ListOfCountries } from '#build/components'; import type { Country
} from '#build/components';
<template>
  List of countries component
  <v-card v-for="country in countries" :key="country.name.official">
    <h4>{{ country.name.official }}</h4>
    <p>{{ country.population }}</p>
    <p>{{ country.region }}</p>
    <p>{{ country.capital }}</p>
  </v-card>
  <!-- <p v-else-if="error">Unable to fetch data. {{ error }}</p> -->
</template>

<script setup lang="ts">
// async function Test() {
//   const result = await fetch("https://restcountries.com/v3.1/all");
//   const all = await result.json();
//   console.log(all);
//   return all;
// }
// const { result } = useFetch(Test);

const { data: countries } = await useFetch(
  "https://restcountries.com/v3.1/all"
);

// Log the result whenever it changes
</script>
