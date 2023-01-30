<script setup>
import HeaderComponent from '@/components/Header.vue'
</script>

<template>
  <HeaderComponent class="container" />

  <main class="container">
    <h1>keyboard</h1>
  </main>
</template>

<style>
@import url('@/styles/reset.css');
@import url('@/styles/variables.css');

body {
  background-color: hsl(var(--background-color));
  color: hsl(var(--text-color));
  font-family: 'Lora', serif;
  /* font-family: 'Roboto', sans-serif; */
  font-size: 1rem;
  transition: color .3s ease-in-out, background-color .3s ease-in-out;
}

.container {
  max-width: 64rem;
  padding-inline: 2em;
  margin-inline: auto;
}
</style>
