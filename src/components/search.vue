<template>
  <div>
    <form>
      <input type="text" placeholder="Search giphy" v-model="tag" />
      <button @click.prevent="search">Search</button>
    </form>
    <!--GIF DISPLAY-->
    <div class="container">
      <div v-if="!loading" class="row">
        <div class="col s12 m3" v-for="gif in gifs" :key="gif.id">
          <img v-bind:src="`${gif.images.preview_gif.url}`" alt="gify" />
        </div>
        <div class="load">
          <button v-if="showLoad" v-on:click="search" style="center-align">
            LOAD MORE
          </button>
        </div>
      </div>
      <div v-else>
        <p>Loading....</p>
      </div>
    </div>
  </div>
</template>

<script>
require("dotenv").config();
console.log(process.env);
import axios from "axios";
export default {
  name: "search",
  data() {
    return {
      loading: false,
      limit: 18,
      tag: "",
      gifs: [],
      showLoad: false,
    };
  },
  methods: {
    loadmore() {
      this.fetchImages().then((response) => {
        this.gifs.push(response.data.data);
        console.log(this.gifs);
      });
    },
    search() {
      this.loading = true;
      this.fetchImages().then((response) => {
        this.gifs = response.data.data;
        console.log(response.data);
        this.loading = false;
        this.limit += 18;
      });
    },
    fetchImages() {
      return axios({
        method: "get",
        url: "https://api.giphy.com/v1/gifs/search",
        params: {
          api_key: "TvHGP2bAbcXxa8Rc2Sfs9mHzweDa4LsG",
          q: this.tag,
          limit: this.limit,
          offset: 0,
        },
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin-left: 80px;
}
.img {
  border: 10px solid #ddd;
  border-radius: 4px;
  padding: 5px;
  width: 150px;
}
</style>
