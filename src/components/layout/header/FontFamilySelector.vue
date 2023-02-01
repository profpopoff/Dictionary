<script setup>
import { ref } from 'vue'

const selectedFont = ref('Serif')

const fonts = ref([
   { text: 'Serif', value: 'Serif' },
   { text: 'Sans Serif', value: 'Sans Serif' }
])
</script>

<template>
   <!-- <select v-model="selectedFont">
      <option v-for="font in fonts" :value="font.value">
         {{ font.text }}
      </option>
   </select> -->
   <span>Serif</span>
</template>