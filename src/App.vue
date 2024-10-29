<script setup>
// import GithubCard from '@/components/GithubCard.vue'
import AppAlert from '@/components/AppAlert.vue'
import MyInput from '@/components/MyInput.vue'
import { onMounted, onUnmounted, ref } from 'vue'
import MouseCoordinates from '@/components/MouseCoordinates.vue'

// const usernames = ['danielkellyio', 'hootlex', 'MooseSaeed', 'JesusGarciaValadez']
const alerts = ref([
  { type: 'info', message: 'New software update available.' },
  { type: 'success', message: 'Your purchase has been confirmed.' },
  { type: 'warning', message: 'Warning: Invalid email address.' },
  { type: 'error', message: 'Error! Task failed successully.' },
])
const model = ref('')
const input = ref(null)
const screenSize = window.innerWidth

const onKeyPress = (e) => {
  if (e.key === '/') {
    e.preventDefault()

    input.value.input.focus()
  }
}

onMounted(() => {
  document.body.addEventListener('keypress',onKeyPress )
})

onUnmounted(() => {
  document.body.removeEventListener('keypress', onKeyPress)
})
</script>

<template>
  <MouseCoordinates v-slot="{ x, y }">
    <div class="fixed top-0 right-0 p-5 text-white">
      <p>Mouse coordinates: {{ x }}, {{ y }}</p>
    </div>
    <div class="container">
      <div class="left">
        <button v-if="(screenSize / 2) < x">Left</button>
      </div>
      <div class="right">
        <button v-if="(screenSize / 2) > x">Right</button>
      </div>
    </div>
  </MouseCoordinates>
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

    <MyInput v-model:model="model" ref="input" />
    <pre class="text-white">
      {{ model }}
    </pre>
  </div>
</template>
