<script setup>
import { ref } from 'vue'

const hover = ref(false)
</script>

<template>
  <button class="fancy-button" @mouseenter="$event => hover = true" @mouseleave="$event => hover = false">
    <slot name="icon" :hover="hover" random="hello">-</slot>
    <slot>Click Me</slot>
  </button>
  {{ hover}}
</template>
