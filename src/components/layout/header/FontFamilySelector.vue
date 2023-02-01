<script setup>
import ArrowDownIcon from '../../icons/ArrowDownIcon.vue'
import { onMounted, ref } from 'vue'

const selectedFont = ref('serif')

const fonts = ref([
   { text: 'Serif', value: 'serif' },
   { text: 'Sans Serif', value: 'sans-serif' }
])

onMounted(() => {
   if (!!localStorage.getItem('isSans')) {
      selectedFont.value = 'sans-serif'
      document.body.classList.add(selectedFont.value)
   }
})

const changeHandle = () => {
   if (selectedFont.value === 'sans-serif') {
      document.body.classList.add(selectedFont.value)
      localStorage.setItem('isSans', true)
   } else {
      document.body.classList.remove('sans-serif')
      localStorage.removeItem('isSans')
   }
}
</script>

<template>
   <div class="select">
      <select v-model="selectedFont" @change="changeHandle">
         <option v-for="font in fonts" :value="font.value">
            {{ font.text }}
         </option>
      </select>
      <ArrowDownIcon class="icon" />
   </div>
</template>

<style scoped>
.select {
   position: relative;
}

.select:hover .icon {
   transform: rotate(90deg);
}

select {
   padding-block: .5em;
   padding-right: 2em;
   border: none;
   background-color: hsl(var(--background-color));
   cursor: pointer;
   text-align: end;
   font-size: .95em;
   font-weight: 700;
   transition: var(--dark-theme-transition);
   appearance: none;
}

option {
   font-weight: 400;
}

.icon {
   position: absolute;
   right: 0;
   width: 1em;
   pointer-events: none;
   color: hsl(var(--accent-color));
   transition: transform .3s ease-in-out;
}
</style>