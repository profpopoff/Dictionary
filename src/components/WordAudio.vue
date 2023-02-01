<script setup>
import { onMounted, ref } from 'vue'
import CustomPlayButton from './ui/CustomPlayButton.vue'

const props = defineProps({
   phonetics: Array
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
   <audio v-if="!!phonetics[0].audio" :src="phonetics[0].audio" @ended="isPlaying = !isPlaying" ref="audio"></audio>
   <audio v-else-if="!!phonetics[1].audio" :src="phonetics[1].audio" @ended="isPlaying = !isPlaying"
      ref="audio"></audio>
   <audio v-else-if="!!phonetics[2].audio" :src="phonetics[2].audio" @ended="isPlaying = !isPlaying"
      ref="audio"></audio>
   <CustomPlayButton @click="audioClickHandle" :isPlaying="isPlaying" />
</template>