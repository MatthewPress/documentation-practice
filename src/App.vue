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
    releases.value = await res.data.json()
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
      <article key={{ release.index }}>
        <h2>{{ release.id }}</h2>
      </article>
    </section>
  </main>
</template>

<style scoped>
article {
  background-color: white;
  height: 5rem;
  width: 5rem;
}
</style>
