<script setup>
import { marked } from 'marked';
const props = defineProps({
  release: { required: true }
})
console.log(marked.parse(props?.release.body))
</script>
<template>
  <article>
    <h2>{{ release.name }}</h2>
    <p>{{ release.tag_name }} | {{ release.published_at }}</p>
    <hr />
    {{ marked.parse(props?.release.body) }}
  </article>
</template>
<style scoped>
article {
  background-color: white;
  color: black;
  display: flex;
  flex-direction: column;
  margin: 10px;
  border: 5px solid black;
  border-radius: 10px;
  max-width: 50%;
}
</style>