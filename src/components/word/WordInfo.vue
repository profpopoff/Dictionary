<script setup>
const props = defineProps({
   word: {
      type: String,
      required: true
   },
   phonetics: {
      type: Array,
      required: true
   },
})
</script>

<template>
   <div class="info">
      <h1>{{ word }}</h1>
      <div class="phonetics">
         <h3 v-for="phonetic in phonetics">{{
            phonetic
         }}</h3>
      </div>
   </div>
</template>

<style scoped>
.info {
   display: flex;
   flex-direction: column;
   gap: .5em;
}

.info h1 {
   font-size: 3em;
}

.info h3 {
   font-family: 'Roboto', sans-serif;
   font-weight: 400;
   color: hsl(var(--accent-color));
}

.phonetics {
   display: flex;
   gap: .5em 1.5em;
   flex-wrap: wrap;
}
</style>