<script setup>
import Definition from './Definition.vue'

const props = defineProps({
   meaning: Object
})
</script>

<template>
   <div class="meaning">
      <h2><span>{{ meaning.partOfSpeech }}</span></h2>
      <h3>Meaning</h3>
      <ul class="definitions">
         <Definition v-for="definition in meaning.definitions" :definition="definition" />
      </ul>
      <div class="synonyms" v-if="meaning.synonyms.length">
         <h3>Synonym<span v-if="meaning.synonyms.length > 1">s</span></h3>
         <h3 class="synonym" v-for="synonym in meaning.synonyms">{{ synonym }}</h3>
      </div>
   </div>
</template>

<style scoped>
.meaning {
   display: flex;
   flex-direction: column;
   gap: 1.75em;
}

h2 {
   position: relative;
   display: block;
   font-style: italic;
}

h2 span {
   position: relative;
   width: min-content;
}

h2 span::before {
   content: "";
   position: absolute;
   inset: 0 -1em 0 0;
   z-index: -1;
   background-color: hsl(var(--background-color));
   transition: var(--dark-theme-transition);
}

h2::after {
   content: "";
   position: absolute;
   top: 50%;
   right: 0;
   width: 100%;
   height: 1px;
   z-index: -2;
   background-color: hsl(var(--text-color) / .25);
   transition: var(--dark-theme-transition);
}

h3 {
   color: hsl(var(--text-color) / .5);
   font-weight: 400;
   transition: var(--dark-theme-transition);
}

.definitions {
   list-style: none;
   display: flex;
   flex-direction: column;
   gap: 1em;
}

.synonyms {
   display: flex;
   gap: 1.5em;
}

.synonym {
   color: hsl(var(--accent-color));
   font-weight: 700;
}
</style>