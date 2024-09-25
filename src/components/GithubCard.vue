<script setup lang="ts">
import { onBeforeMount, Ref, ref } from 'vue'

// Define the type of the username object
type Username = {
  avatar_url: string
  login: string
  name: string
  followers: number
  following: number
  html_url: string
}

const props = defineProps({
  username: {
    type: String,
    required: true,
    default: '',
  },
})

const user: Ref<Username> = ref(null)

onBeforeMount(async () => {
  const response = await fetch(`https://api.github.com/users/${props.username}`)
  user.value = await response.json()
})
</script>

<template>
  <div v-if="user" class="m-5 card card-side bg-base-100 shadow-xl">
    <figure>
      <img :src="user.avatar_url"
           :alt="`Github ${user.login} profile photo`">
    </figure>
    <div class="card-body">
      <h2 class="card-title">{{ user?.name }}</h2>
      <p><strong>Followers:</strong> {{ user?.followers }} <strong>Following:</strong> {{ user?.following }}</p>
      <div class="card-actions justify-end">
        <a :href="user?.html_url" class="btn btn-primary">View profile</a>
      </div>
    </div>
  </div>
</template>
