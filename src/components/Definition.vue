<script setup>
const props = defineProps({
   definition: Object
})
</script>

<template>
   <li>
      <span>{{ definition.definition }}</span>
      <span class="example" v-if="definition.example">"{{ definition.example }}"</span>
   </li>
</template>

<style scoped>
li {
   font-size: 1.1em;
}

.example {
   display: block;
   padding-top: .5rem;
   color: hsl(var(--text-color) / .5);
   transition: var(--dark-theme-transition);
}

li::before {
   content: "\2022";
   color: hsl(var(--accent-color));
   font-weight: bold;
   display: inline-block;
   width: 1em;
   margin-left: -1em;
   transform: translateX(-.3em);
}
</style>