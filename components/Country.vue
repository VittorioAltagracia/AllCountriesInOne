<template>
  <main>
    <div>
      <v-img
        :width="350"
        :height="190"
        aspect-ratio="16/9"
        cover
        :alt="countryInfo.flags?.alt"
        :src="countryInfo.flags?.png"
      >
      </v-img>
    </div>
    <div>
      <h3>{{ countryInfo.name.common }}</h3>
      <p>Native Name:{{ countryInfo.name.nativeName }}</p>

      <p>Population: {{ countryInfo.population }}</p>
      <p>Region: {{ countryInfo.region }}</p>
      <p>Sub Region: {{ countryInfo.subregion }}</p>

      <p>Capital: {{ countryInfo.capital }}</p>
      <p v-if="countryInfo.currencies">
        Currencies:
        <span v-for="(currency, key) in countryInfo.currencies" :key="key">
          {{ currency.name }} ({{ key }})
        </span>
      </p>
      <p>Languages: {{ countryInfo.languages }}</p>
    </div>
  </main>
</template>

<script setup lang="ts">
const route = useRoute();
const countryToGet = route.params.country;
let countryInfo = useState("country info", () => ({}));

console.log(countryToGet);

const getCountry = async () => {
  const response = await fetch(
    `https://restcountries.com/v3.1/name/${countryToGet}`
  );
  const fetchedCountry = await response.json();
  countryInfo.value = fetchedCountry[0];
  console.log(fetchedCountry);
};
getCountry();

watch(
  () => route.params.country,
  (newValue) => {
    countryToGet.value = newValue;
    getCountry();
  }
);
</script>
