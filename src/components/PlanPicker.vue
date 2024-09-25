<script setup>
import CoffeePlan from '@/components/CoffeePlan.vue'
import { onUnmounted, ref } from 'vue'

defineProps({
  plans: {
    type: Array,
    required: true,
    default: () => ['Plan 1', 'Plan 2', 'Plan 3'],
  },
})

const selectedCoffeePlan = ref()

function handleSelectCoffeePlan(name) {
  selectedCoffeePlan.value = name
}

onUnmounted(() => {
  console.log('Bye bye plan picker')
})
</script>

<template>
  <div class="plans">
    {{ selectedCoffeePlan}}
    <CoffeePlan v-for="plan in plans"
                :key="plan"
                :name="plan"
                :selected="plan === selectedCoffeePlan"
                @selected="handleSelectCoffeePlan"
    />
  </div>
</template>
