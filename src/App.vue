<script setup>
import { ref } from 'vue'
import axios from 'axios'

// Where do I get the correct access token?
let http = axios.create({
  baseURL: "https://api.github.com/repos/MatthewPress/documentation-practice/releases",
  headers: {
    "Content-type": "application/json",
    "Authorization": `Bearer ${process.env.VUE_APP_GITHUB_TOKEN}` 
  }
});

let releases = ref([]);

async function getReleases() {
  try {
    const res = await http.get()
    releases.value = res.data
    console.log(releases.value)
  } catch (err) {
    console.log(err.message)
  }
}

</script>

<template>
  <header>
  </header>

  <main>
    <button @click="getReleases">Get Releases</button>
    <section v-for="(release, index) in releases">
      <article>
        <h2>{{ release.name }}</h2>
        <h3>{{ release.body }}</h3>
        <p>{{ release.tag_name }}</p>
        <p>{{ release.published_at }}</p>
      </article>
    </section>
  </main>
</template>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  margin: 10px;
}
article {
  background-color: white;
  color: black;
  display: flex;
  flex-direction: column;
  margin: 10px;
}
</style>
