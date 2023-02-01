<script setup>
import WordAudio from './WordAudio.vue'
import WordInfo from './WordInfo.vue';
import WordMeaning from './WordMeaning.vue'

const props = defineProps({
   wordInfo: Object
})

</script>

<template>
   <div class="word">
      <div class="headline">
         <WordInfo :word="wordInfo.word"
            :phonetics="[...new Set(wordInfo.phonetics.map(({ text }) => text).filter(notEmpty => notEmpty))]" />
         <WordAudio :audios="wordInfo.phonetics.map(({ audio }) => audio).filter(notEmpty => notEmpty)" />
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
.word {
   display: flex;
   flex-direction: column;
   gap: 2em;
}

.headline {
   display: flex;
   justify-content: space-between;
   align-items: center;
   gap: 3em;
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