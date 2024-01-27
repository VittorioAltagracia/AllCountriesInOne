<template>
  <v-container fluid>
    <v-row>
      <v-col
        v-for="(countryGroup, index) in countryGroups"
        :key="index"
        xs="12"
        md="3"
        class="d-flex flex-wrap"
      >
        <v-card v-for="country in countryGroup" :key="country.name.common">
          <NuxtLink :to="`/${country.name.common}`">
            <v-img
              :width="350"
              :height="190"
              aspect-ratio="16/9"
              cover
              :alt="country.flags.alt"
              :src="country.flags.png"
            >
            </v-img>
            <h4>{{ country.name.common }}</h4>
            <p>Population: {{ country.population }}</p>
            <p>Region: {{ country.region }}</p>
            <p>Capital: {{ country.capital }}</p>
          </NuxtLink>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";

const countries = ref([]);
const countryGroups = ref([[], [], [], []]);

const fetchCountries = async () => {
  const response = await fetch("https://restcountries.com/v3.1/all");
  const allCountries = await response.json();
  countries.value = allCountries;
  const group = Math.ceil(allCountries.length / 4);
  for (let i = 0; i < 4; i++) {
    countryGroups.value[i] = allCountries.slice(i * group, (i + 1) * group);
  }
};

onMounted(fetchCountries);

console.log(countries);
// Log the result whenever it changes
</script>
