<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import { ref } from 'vue'

function getReleases() {
  fetch()
}

</script>

<template>
  <header>
  </header>

  <main>
    <button @click="getReleases">Get Releases</button>
  </main>
</template>

<style scoped>
</style>
