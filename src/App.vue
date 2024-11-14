<script setup>
import { onMounted, ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

const message = ref('')
onMounted(() => {
  fetch('https://hono-vercel-eight.vercel.app/api').then((res) => {
    if(!res.ok) {
      console.error('Response is not ok', res);
      return
    }
    return res.json()
  }).then(data => {
    if(!data || typeof data !== 'object' || !('message' in data) || typeof data.message !== 'string') {
      console.error('Invalid response data', data);
      return
    }
    message.value = data.message
  })
})
</script>

<template>
  <div>
    <a href="https://vite.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld :msg="message" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
