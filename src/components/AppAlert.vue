<script setup>
import IconError from '@/components/icons/IconError.vue'
import IconInfo from '@/components/icons/IconInfo.vue'
import IconSuccess from '@/components/icons/IconSuccess.vue'
import IconWarning from '@/components/icons/IconWarning.vue'
import { computed, ref } from 'vue'
const props = defineProps({
  type: {
    type: String,
    required: true,
    default: 'info',
  },
})

const alertType = computed(() => {
  return {
    info: 'alert-info',
    success: 'alert-success',
    warning: 'alert-warning',
    error: 'alert-error',
  }[props.type]
})

const icon = computed(() => {
  return {
    info: IconInfo,
    success: IconSuccess,
    warning: IconWarning,
    error: IconError,
  }[props.type]
})

const color = computed(() => {
  return {
    info: 'text-white',
    success: 'text-white',
    warning: 'text-black',
    error: 'text-white',
  }[props.type]
})

const emit = defineEmits(['closed'])

const closed = ref(false)
function close() {
  closed.value = true
  emit('closed')
}
</script>

<template>
  <div v-if="!closed" role="alert" :class="`alert ${alertType}`">
    <component :is="icon" class="mr-2"></component>
    <span :class="color"><slot></slot></span>
    <button type="button" class="close" data-dismiss="alert" aria-label="Close" @click="close">
      <span aria-hidden="true">&times;</span>
    </button>
  </div>
</template>
