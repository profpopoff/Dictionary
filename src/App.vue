<script setup>
import { ref } from 'vue'
import HeaderComponent from '@/components/Header.vue'
import SearchBar from './components/SearchBar.vue'

const definition = ref('')

const getDefinition = async (word) => {
  if (!!word) {
    await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`)
      .then(response => response.json())
      .then(data => definition.value = data)
  } else {
    definition.value = ''
  }
}
</script>

<template>
  <HeaderComponent class="container" />

  <main class="container">
    <SearchBar @get-word="getDefinition" />
    <h1 v-if="definition.length">{{ definition[0].word }}</h1>
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
