<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import { ref } from 'vue'

let count = ref(0)

</script>

<template>
  <header>
  </header>

  <main>
    <button @click="count++">{{ count }}</button>
  </main>
</template>

<style scoped>
</style>
