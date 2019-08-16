<template>
  <div class="container">
    <form class="searchbar" @submit.prevent="newSearch(searchTerm)">
      <input v-model="searchTerm" type="text" class="searchform">
      <input type="submit" value="Search" class="searchbutton">
    </form>

    <div class="gallery">
      <a v-for="post in results" :key="post.id" :href="post.file_url" class="post_preview">
        <img :src="post.sample_url">
      </a>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
const request = require("request");

import Gallery from "./Gallery.vue";

@Component
export default class E621Search extends Vue {
  searchTerm: string = "";
  results: any[] = [];
  page = 0;

  newSearch(searchTerm: string) {
    this.clearResults();
    this.search(searchTerm);
  }

  search(searchTerm: string, page = 0, limit = 50) {
    request.get(
      {
        url:
          `https://www.e621.net/post/index.json` +
          `?tags=${searchTerm}` +
          `&limit=${limit}` +
          `&page=${page}`,
        headers: {
          "User-Agent": "Custom E6 viewer V0.0.0 <notandinotandi@gmail.com>"
        }
      },
      (err: any, resp: any, body: any) => {
        if (err) throw err;
        let posts = JSON.parse(body);
        console.log(posts[0]);
        this.results = [...this.results, ...posts];
      }
    );
  }

  clearResults() {
    this.results = [];
    this.page = 0;
  }
}
</script>

<style lang="scss" scoped>
.searchbar {
  display: fixed;
  flex-direction: row;
  height: 64px;
  width: 100vw;
  input {
    border-radius: 0;
    border: none;
    height: 100%;
    padding: 0;
  }
  .searchform {
    flex-grow: 1;
  }
}

.gallery {
  margin-top: 64px;
  width: 100%;
}
</style>
