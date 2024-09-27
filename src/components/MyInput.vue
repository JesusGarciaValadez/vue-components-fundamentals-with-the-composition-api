<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  model: {
    type: String,
    required: true,
  },
})
const input = ref(null)
const _model = ref(props.model)

defineExpose({
  input
})

const $emit = defineEmits(['update:model'])

watch(_model, (value) => {
  $emit('update:model', value)
})
</script>

<template>
  <input type="text" v-model="_model" ref="input" />
</template>
