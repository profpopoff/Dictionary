<script setup>
import { onMounted, ref } from 'vue'
import CustomPlayButton from './ui/CustomPlayButton.vue'

const props = defineProps({
   audios: {
      type: Array,
      required: true
   }
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
   <div v-if="!!audios.length">
      <audio v-if="!!audios[0]" :src="audios[0]" @ended="isPlaying = !isPlaying" ref="audio"></audio>
      <CustomPlayButton @click="audioClickHandle" :isPlaying="isPlaying" />
   </div>
</template>