<script setup>
import { ref } from 'vue'
import SearchIcon from './icons/SearchIcon.vue'

const word = ref('')
</script>

<template>
   <form class="search-bar" @submit.prevent="$emit('getWord', word)">
      <input class="search-bar__input" type="text" placeholder="Search..." v-model="word">
      <button class="search-bar__button" type="submit">
         <SearchIcon width="40%" />
      </button>
   </form>
</template>

<style scoped>
.search-bar {
   height: 4em;
   width: auto;
   display: flex;
   align-items: center;
   border-radius: 1em;
   overflow: hidden;
}

.search-bar__input {
   height: 100%;
   flex: 1;
   width: 0;
   padding-left: 1.25em;
   background-color: hsl(var(--grey-color) / .25);
   border: none;
   outline: none;
   color: hsl(var(--text-color));
   font-size: 1.3em;
   font-weight: 700;
   transition: var(--dark-theme-transition);
}

.search-bar__button {
   height: 100%;
   aspect-ratio: 1;
   display: flex;
   justify-content: center;
   background-color: hsl(var(--grey-color) / .25);
   border: none;
   color: hsl(var(--accent-color));
   cursor: pointer;
}

.search-bar__button>* {
   transition: transform .3s ease-in-out;
}

.search-bar__button:hover>* {
   transform: rotate(10deg) scale(1.1);
}
</style>