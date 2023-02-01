<template>
   <span class="loader"></span>
</template>

<style scoped>
.loader {
   width: 3em;
   height: 3em;
   display: block;
   margin: 1em auto;
   position: relative;
   color: #FFF;
   box-sizing: border-box;
   animation: rotation 1s linear infinite;
}

.loader::after,
.loader::before {
   content: '';
   box-sizing: border-box;
   position: absolute;
   width: 1.5em;
   height: 1.5em;
   top: 0;
   background-color: hsl(var(--text-color) / .5);
   border-radius: 50%;
   animation: scale50 1s infinite ease-in-out;
}

.loader::before {
   top: auto;
   bottom: 0;
   background-color: hsl(var(--accent-color));
   animation-delay: 0.5s;
}

@keyframes rotation {
   0% {
      transform: rotate(0deg);
   }

   100% {
      transform: rotate(360deg);
   }
}

@keyframes scale50 {

   0%,
   100% {
      transform: scale(0);
   }

   50% {
      transform: scale(1);
   }
}
</style>