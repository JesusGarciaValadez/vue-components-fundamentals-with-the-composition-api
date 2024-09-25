<script setup>
// import GithubCard from '@/components/GithubCard.vue'
import AppAlert from '@/components/AppAlert.vue'
import MyInput from '@/components/MyInput.vue'
import { onMounted, onUnmounted, ref, useTemplateRef } from 'vue'

// const usernames = ['danielkellyio', 'hootlex', 'MooseSaeed', 'JesusGarciaValadez']
const alerts = ref([
  { type: 'info', message: 'New software update available.' },
  { type: 'success', message: 'Your purchase has been confirmed.' },
  { type: 'warning', message: 'Warning: Invalid email address.' },
  { type: 'error', message: 'Error! Task failed successully.' },
])

const model = ref('')

const input = useTemplateRef('my-input')

onMounted(() => {
  document.body.addEventListener('keypress', (e) => {
    if (e.key === '/') {
      input.value.input.focus()
    }
  })
})

onUnmounted(() => {
  document.body.removeEventListener('keypress', (e) => {
    if (e.key === '/') {
      input.value.input.focus()
    }
  })
})

const handleSearch = (value) => {
  model.value = value
}
</script>

<template>
  <!--GithubCard v-for="(username, index) in usernames"
              :key="`${username}-${index}`"
              :username="username"
  /-->
  <div class="p-5">
    <app-alert v-for="({ type, message }, index) in alerts"
               :key="`${type}-${index}`"
               :type="type"
                @closed="$event => alerts = alerts.filter((a) => a.message !== message)"
    >
      {{ message }}
    </app-alert>

    <pre>{{ alerts }}</pre>

    <MyInput ref="my-input" :model="model" @update:model="handleSearch" />
    <pre class="text-white">
      {{ model }}
    </pre>
  </div>
</template>
