<script setup>
import { ref } from 'vue'
import HeaderComponent from '@/components/AppHeader.vue'
import SearchBar from '@/components/SearchBar.vue'
import AppWord from '@/components/AppWord.vue'

const wordInfo = ref('')
const isLoading = ref(false)

const getWordInfo = async (word) => {
  if (!!word) {
    isLoading.value = true
    await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`)
      .then(response => response.json())
      .then(data => wordInfo.value = data)
    isLoading.value = false
  } else {
    wordInfo.value = ''
  }
}
</script>

<template>
  <HeaderComponent class="container" />

  <main class="container">
    <SearchBar @get-word="getWordInfo" />
    <AppWord v-if="wordInfo[0]" :wordInfo="wordInfo[0]" />
    <h1 v-else-if="wordInfo.message">{{ wordInfo.message }}</h1>
    <h2 v-else-if="isLoading">loading</h2>
    <h2 v-else>ИСкать тут ^</h2>
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
