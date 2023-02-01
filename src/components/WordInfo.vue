<script setup>
import { onMounted, ref } from 'vue'
import WordMeaning from './WordMeaning.vue'
import CustomPlayButton from './ui/CustomPlayButton.vue'

const props = defineProps({
   wordInfo: Object
})

const audio = ref(null)
const isPlaying = ref(false)

onMounted(() => {
   audio.value.focus()
})

const audioClickHandle = () => {
   isPlaying.value = !isPlaying.value

   if (audio.value.paused) {
      audio.value.play()
   } else {
      audio.value.pause()
   }
}
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
         <audio v-if="!!wordInfo.phonetics[0].audio" :src="wordInfo.phonetics[0].audio" @ended="isPlaying = !isPlaying"
            ref="audio"></audio>
         <audio v-else-if="!!wordInfo.phonetics[1].audio" :src="wordInfo.phonetics[1].audio"
            @ended="isPlaying = !isPlaying" ref="audio"></audio>
         <audio v-else-if="!!wordInfo.phonetics[2].audio" :src="wordInfo.phonetics[2].audio"
            @ended="isPlaying = !isPlaying" ref="audio"></audio>
         <CustomPlayButton @click="audioClickHandle" :isPlaying="isPlaying" />
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

.word>div:first-child {
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