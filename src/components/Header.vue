<script setup>
import DarkModeToggle from './DarkModeToggle.vue'
import Logo from './icons/Logo.vue'
</script>

<template>
   <header>
      <Logo />
      <DarkModeToggle />
   </header>
</template>

<style scoped>
header {
   padding-block: 2.5em;
   display: flex;
   justify-content: space-between;
}
</style>