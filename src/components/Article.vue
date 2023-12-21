<script setup>
const props = defineProps({
  release: { required: true }
})
</script>
<template>
  <article>
    <h2>{{ release.name }}</h2>
    <p>{{ release.tag_name }} | {{ release.published_at }}</p>
    <hr />
    <h3>{{ release.body }}</h3>
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
}
</style>