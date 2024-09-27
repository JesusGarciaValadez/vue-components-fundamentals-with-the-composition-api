<script setup>
import { ref, onMounted } from 'vue'

const x = ref(0)
const y = ref(0)

onMounted(() => {
  window.addEventListener('mousemove', (event) => {
    x.value = event.clientX
    y.value = event.clientY
  })
})
</script>

<template>
  <slot :x="x" :y="y" />
</template>

<style scoped>

</style>
