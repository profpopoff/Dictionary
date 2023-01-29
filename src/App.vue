<script setup>
import DarkModeToggle from './components/DarkModeToggle.vue'
</script>

<template>
  <header>
    <h2>header</h2>
  </header>

  <main>
    <h1>main</h1>
    <DarkModeToggle />
  </main>
</template>

<style>
@import url('./styles/reset.css');
@import url('./styles/variables.css');

body {
  background-color: hsl(var(--background-color));
  color: hsl(var(--text-color));
  transition: color .3s ease-in-out, background-color .3s ease-in-out;
}
</style>
