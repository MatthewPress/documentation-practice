<script setup>
import { ref } from 'vue'
import axios from 'axios'
import Article from './components/Article.vue';

// Where do I get the correct access token?
const githubHttp = axios.create({
  baseURL: "https://api.github.com/repos/MatthewPress/documentation-practice/releases",
  headers: {
    "Content-type": "application/json",
    "Authorization": `Bearer ${process.env.VUE_APP_GITHUB_TOKEN}` 
  }
});

const jiraHttp = axios.create({
  baseURL: "https://api.github.com/repos/MatthewPress/documentation-practice/releases",
  headers: {
    "Content-type": "application/json",
    "Authorization": `Bearer ${process.env.VUE_APP_GITHUB_TOKEN}` 
  }
});

const sources = ['GitHub', 'Jira'];

const releases = ref([]);

async function getReleases() {
  try {
    const res = await githubHttp.get()
    releases.value = res.data
    console.log(releases.value)
  } catch (err) {
    console.log(err.message)
  }
}

</script>

<template>
  <header>
    <template v-for="(source, index) in sources" :key="index">
      <button @click="getReleases(source)">{{ source }} Releases</button>
    </template>
  </header>

  <main>
    <section v-for="(release, index) in releases" :key="index">
      <Article :release="release"></Article>
    </section>
  </main>
</template>

<style scoped>
header {
  display: flex;
  background-color: black;
  padding: 1rem;
}
section {
  display: flex;
  flex-direction: column;
  margin: 10px;
}
button {
  background-color: white;
  font-weight: bold;
  height: 2rem;
  border: 0px;
  border-radius: 5px;
  margin-right: 1rem;
}
</style>
