<script setup>
// import GithubCard from '@/components/GithubCard.vue'
import AppAlert from '@/components/AppAlert.vue'
import { ref } from 'vue'

// const usernames = ['danielkellyio', 'hootlex', 'MooseSaeed', 'JesusGarciaValadez']
const alerts = ref([
  { type: 'info', message: 'New software update available.' },
  { type: 'success', message: 'Your purchase has been confirmed.' },
  { type: 'warning', message: 'Warning: Invalid email address.' },
  { type: 'error', message: 'Error! Task failed successully.' },
])
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
  </div>
</template>
