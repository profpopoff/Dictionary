<script setup>
import PlayIcon from '../icons/PlayIcon.vue'
import PauseIcon from '../icons/PauseIcon.vue'

const props = defineProps({
   isPlaying: Boolean
})
</script>

<template>
   <button>
      <PlayIcon :class="{ active: !isPlaying }" />
      <PauseIcon :class="{ active: isPlaying }" />
   </button>
</template>

<style scoped>
button {
   flex-shrink: 0;
   width: 5em;
   aspect-ratio: 1;
   border-radius: 50%;
   display: flex;
   justify-content: center;
   align-items: center;
   border: none;
   background-color: hsl(var(--accent-color) / .25);
   color: hsl(var(--accent-color));
   overflow: hidden;
   cursor: pointer;
   position: relative;
}

button>* {
   position: absolute;
   opacity: 0;
   transition: all .15s ease-in-out;
}

.active {
   display: block;
   opacity: 1;
}
</style>