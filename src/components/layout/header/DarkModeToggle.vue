<script setup>
import { useDark, useToggle } from '@vueuse/core'
import CustomToggle from '../../ui/CustomToggle.vue'
import MoonIcon from '../../icons/MoonIcon.vue'

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
   position: relative;
}

.toggle::before {
   content: "";
   position: absolute;
   left: -1.5em;
   height: calc(100% + 1em);
   width: 1px;
   background-color: hsl(var(--grey-color) / .5);
}
</style>