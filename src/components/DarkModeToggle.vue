<script setup>
import { useDark, useToggle } from '@vueuse/core'

const isDark = useDark()
const toggleDark = useToggle(isDark)
</script>

<template>
   <button class="button" @click="toggleDark()">
      Dark mode: {{ isDark }}
   </button>
</template>

<style scoped>
.button {
   color: hsl(var(--accent-color));
   background-color: hsl(var(--text-color));
}
</style>