<script setup>
import { onMounted, ref } from 'vue'
import AppHeader from '@/components/layout/header/AppHeader.vue'
import SearchBar from '@/components/SearchBar.vue'
import AppWord from '@/components/word/AppWord.vue'
import LoadingIndicator from './components/LoadingIndicator.vue'

const wordInfo = ref('')
const isLoading = ref(true)
const fetchError = ref({ status: false, word: '' })

onMounted(async () => {
  await delay(500)
  getWordInfo('dictionary')
})

const getWordInfo = async (word) => {
  const fetchStart = Date.now()
  await fetch(`https://api.dictionaryapi.dev/api/v2/entries/en/${word}`)
    .then(response => response.json())
    .then(data => {
      if (Array.isArray(data)) {
        fetchError.value = { status: false, word: '' }
        wordInfo.value = data
      } else {
        throw new Error
      }
    })
    .catch(() => fetchError.value = { status: true, word })
    .finally(() => isLoading.value = false)
  const fetchTime = Date.now() - fetchStart
  if (fetchTime > 250) {
    isLoading.value = true
    await delay(750)
    isLoading.value = false
  }
}

const delay = ms => {
  return new Promise(resolve => setTimeout(resolve, ms))
}
</script>

<template>
  <AppHeader class="container" />
  <main class="container">
    <SearchBar @get-word="getWordInfo" />
    <h2 class="error" v-if="fetchError.status">Sorry, but&nbsp;we couldn&rsquo;t find definitions for the word &laquo;<span>{{
      fetchError.word
    }}</span>&raquo;.</h2>
    <LoadingIndicator v-else-if="isLoading" />
    <AppWord v-else-if="wordInfo[0]" :wordInfo="wordInfo[0]" />
  </main>
</template>

<style>
@import url('@/styles/reset.css');
@import url('@/styles/variables.css');

body {
  background-color: hsl(var(--background-color));
  color: hsl(var(--text-color));
  font-family: 'Lora', serif;
  font-size: clamp(.7rem, 3vw, 1rem);
  transition: var(--dark-theme-transition);
}

body.sans {
  font-family: 'Roboto', sans-serif;
}

body.mono {
  font-family: 'Roboto Mono', monospace;
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
}

.error {
  font-size: 1.7em;
  text-align: center;
}

.error span {
  color: hsl(var(--accent-color));
}
</style>
