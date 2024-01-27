<template>
  <country />
  <NuxtLink to="/">
    <v-btn>Back</v-btn>
  </NuxtLink>
</template>

<script setup lang="ts">
definePageMeta({
  layout: "country",
});
</script>
