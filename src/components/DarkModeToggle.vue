<script setup>
import { useDark, useToggle } from '@vueuse/core'
import CustomToggle from './ui/CustomToggle.vue'
import MoonIcon from './icons/MoonIcon.vue'

const isDark = useDark()
const toggleDark = useToggle(isDark)
</script>

<template>
   <CustomToggle class="toggle" @change="toggleDark()" :isChecked="isDark">
      <MoonIcon />
   </CustomToggle>
</template>

<style scoped>
.toggle {
   gap: 1em;
}
</style>