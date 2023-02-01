<script setup>
import { onMounted, ref } from 'vue'
import CustomPlayButton from './ui/CustomPlayButton.vue'

const props = defineProps({
   audios: Array
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
   <audio v-if="!!audios[0]" :src="audios[0]" @ended="isPlaying = !isPlaying" ref="audio"></audio>
   <CustomPlayButton @click="audioClickHandle" :isPlaying="isPlaying" />
</template>