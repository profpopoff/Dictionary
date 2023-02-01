<script setup>
import { ref } from 'vue'
import HeaderComponent from '@/components/AppHeader.vue'
import SearchBar from '@/components/SearchBar.vue'
import AppWord from '@/components/AppWord.vue'
import LoadingIndicator from './components/LoadingIndicator.vue'

const wordInfo = ref('')
const isLoading = ref(false)

const getWordInfo = async (word) => {
  isLoading.value = true
  wordInfo.value = ''
  if (!!word) {
    await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`)
      .then(response => response.json())
      .then(data => wordInfo.value = data)
    isLoading.value = false
  } else {
    wordInfo.value = ''
    isLoading.value = false
  }
}
</script>

<template>
  <HeaderComponent class="container" />

  <main class="container">
    <SearchBar @get-word="getWordInfo" />
    <h1 v-if="wordInfo.message">{{ wordInfo.message }}</h1>
    <AppWord v-else-if="wordInfo[0]" :wordInfo="wordInfo[0]" />
    <LoadingIndicator v-else-if="isLoading" />
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
  transition: var(--dark-theme-transition);
}

.container {
  max-width: 56rem;
  padding-inline: 2em;
  margin-inline: auto;
}

main {
  display: flex;
  flex-direction: column;
  gap: 2em;
  margin-bottom: 5em;
}
</style>
