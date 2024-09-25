<script setup>
import { ref, useTemplateRef, watch } from 'vue'

const props = defineProps({
  model: {
    type: String,
    required: true,
  },
})
const input = useTemplateRef('my-input')
const _model = ref(props.model)

defineExpose({
  model: props.model,
  input
})

const $emit = defineEmits(['update:model'])

watch(_model, (value) => {
  console.log('updateModel', value)
  $emit('update:model', value)
})
</script>

<template>
  <input type="text" v-model="_model" ref="my-input" />
</template>
