<script setup>
import { ref } from 'vue'
import axios from 'axios'

let githubHttp = axios.create({
  baseURL: "https://api.github.com/repos/MatthewPress/documentation-practice/releases",
  headers: {
    "Content-type": "application/json",
    "Authorization": `Bearer ${process.env.VUE_APP_GITHUB_TOKEN}` 
  }
});

let jiraHttp = axios.create({
  baseURL: `https://matthew-press.atlassian.net/rest/api/latest/project/`,
  headers: {
    "Content-type": "application/json",
  }
});

let releases = ref([]);

async function getReleases(source) {
  try {
    const res = await source.get()
    releases.value = res.data
    console.log(releases.value)
  } catch (err) {
    console.log(err.message)
  }
}

</script>

<template>
  <header>
    <button @click="getReleases(githubHttp)">GitHub Releases</button>
    <button @click="getReleases(jiraHttp)">Jira Releases</button>
  </header>

  <main>
    <section v-for="(release, index) in releases">
      <article>
        <h2>{{ release.name }}</h2>
        <p>{{ release.tag_name }} | {{ release.published_at }}</p>
        <hr />
        <p className="release-body">{{ release.body }}</p>
      </article>
    </section>
  </main>
</template>

<style scoped>
header {
  height: 5rem;
  background-color: black;
  padding: 1rem;
}
button {
  height: 2rem;
  background-color: white;
  border-radius: 1rem;
  font-weight: bold;
}
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
  margin: 1rem;
  padding: 1rem;
  border: 0.5rem solid black;
  border-radius: 1rem;
}
.release-body {
  padding: 1rem;
}
</style>
