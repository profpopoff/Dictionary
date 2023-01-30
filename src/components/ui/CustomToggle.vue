<script setup>
const props = defineProps({
   isChecked: {
      type: Boolean,
      default: false,
   }
})
</script>

<template>
   <div class="custom-toggle">
      <input class="custom-toggle__input" type="checkbox" name="toggle" id="toggle" :checked="isChecked">
      <label class="custom-toggle__label" for="toggle">
         <slot />
      </label>
   </div>
</template>

<style scoped>
.custom-toggle {
   display: flex;
   align-items: center;
   gap: .5em;
}

.custom-toggle__label {
   cursor: pointer;
   -webkit-touch-callout: none;
   -webkit-user-select: none;
   -khtml-user-select: none;
   -moz-user-select: none;
   -ms-user-select: none;
   user-select: none;
}

.custom-toggle__input {
   --height: 1.5em;
   --padding: .3em;

   position: relative;
   width: 3em;
   height: var(--height);
   background: hsl(var(--grey-color));
   border-radius: 2em;
   cursor: pointer;
   -webkit-appearance: none;
   -moz-appearance: none;
   appearance: none;
   transition: all 0.3s cubic-bezier(0.2, 0.85, 0.32, 1.4);
}

.custom-toggle__input::after {
   content: "";
   display: inline-block;
   position: absolute;
   left: var(--padding);
   top: 50%;
   width: calc(var(--height) - var(--padding) * 2);
   aspect-ratio: 1;
   background-color: #fff;
   border-radius: 50%;
   transform: translate(0, -50%);
   transition: all 0.3s cubic-bezier(0.2, 0.85, 0.32, 1.4);
}

.custom-toggle__input:checked {
   background-color: hsl(var(--accent-color));
}

.custom-toggle__input:checked::after {
   left: calc(100% - (var(--height) - var(--padding)));
}
</style>