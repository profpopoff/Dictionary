<script setup>
import LogoIcon from './icons/LogoIcon.vue'
import FontFamilySelector from './FontFamilySelector.vue'
import DarkModeToggle from './DarkModeToggle.vue'
</script>

<template>
   <header>
      <LogoIcon />
      <div>
         <FontFamilySelector />
         <DarkModeToggle />
      </div>
   </header>
</template>

<style scoped>
header {
   padding-block: 2.5em;
   display: flex;
   justify-content: space-between;
   align-items: center;
}

header div {
   display: flex;
   align-items: center;
   gap: 3em;
}
</style>