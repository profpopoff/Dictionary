<script setup>
import WordAudio from './WordAudio.vue'
import WordMeaning from './WordMeaning.vue'

const props = defineProps({
   wordInfo: Object
})

</script>

<template>
   <div class="word-info">
      <div class="word">
         <div>
            <h1>{{ wordInfo.word }}</h1>
            <h3 v-if="!!wordInfo.phonetic">{{ wordInfo.phonetic }}</h3>
            <h3 v-else-if="!!wordInfo.phonetics[0].text">{{
               wordInfo.phonetics[0].text
            }}</h3>
            <h3 v-else-if="!!wordInfo.phonetics[1].text">{{
               wordInfo.phonetics[1].text
            }}</h3>
            <h3 v-else-if="!!wordInfo.phonetics[2].text">{{
               wordInfo.phonetics[2].text
            }}</h3>
         </div>
         <WordAudio :phonetics="wordInfo.phonetics" />
      </div>
      <div class="meanings">
         <WordMeaning v-for="meaning in wordInfo.meanings" :meaning="meaning" />
      </div>
      <div class="source">
         <span>Source</span> <a :href="wordInfo.sourceUrls[0]">{{ wordInfo.sourceUrls[0] }}</a>
      </div>
   </div>
</template>

<style scoped>
.word-info {
   display: flex;
   flex-direction: column;
   gap: 2em;
}

.word {
   display: flex;
   justify-content: space-between;
   align-items: center;
}

.word>div {
   display: flex;
   flex-direction: column;
   gap: .5em;
}

.word h1 {
   font-size: 3em;
}

.word h3 {
   font-family: 'Roboto', sans-serif;
   font-weight: 400;
   color: hsl(var(--accent-color));
}

.meanings {
   display: flex;
   flex-direction: column;
   gap: 2em;
}

.source {
   display: flex;
   gap: 2em;
   border-top: 1px solid hsl(var(--text-color) / .25);
   color: hsl(var(--text-color) / .5);
   padding-top: 1.5em;
   transition: var(--dark-theme-transition), border-color .3s ease-in-out;
}

.source a {
   color: hsl(var(--text-color));
   transition: var(--dark-theme-transition);
}
</style>