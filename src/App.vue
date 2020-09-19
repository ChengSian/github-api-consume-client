<template>
  <div id="app">
    <section class="g-img1">閻承賢的 Github repos</section>

    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <button v-on:click="fetchData">refresh</button>

    <ul class="listing">
      <li v-for="repo in repos" :key="repo.full_name">
        <h2>{{ repo.full_name }}</h2>
        <div class="body">
          <p>{{ repo.description || "This repo not have description!" }}</p>
        </div>
        <div class="cta"><a v-bind:href="repo.html_url">go to github!</a></div>
      </li>
    </ul>
  </div>
</template>

<script>
//import HelloWorld from "./components/HelloWorld.vue";
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";

Vue.use(VueAxios, axios);
var apiURL = "https://api.github.com/users/chengsian/repos";
export default {
  name: "App",
  /* components: {
     HelloWorld,
  }, */
  data() {
    return {
      repos: null,
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      Vue.axios.get(apiURL).then((response) => {
        this.repos = response.data;
        console.log(this.repos);
      });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  box-sizing: border-box;
}
/* img {
  max-width: 100%;
  display: block;
} */
section {
  height: 100vh;

  background: rgba(0, 0, 0, 0.7);
  color: #fff;
  line-height: 100vh;
  text-align: center;
  font-size: 20vh;
  overflow: auto;
}
body {
  font: 1.2em Helvetica, arial, sans-serif;
  padding: 0px;
  margin: 0px;
}

.g-img1 {
  background-image: url("http://up.enterdesk.com/edpic_source/21/00/00/210000f8e772d7fc0758e67ae4b48807.jpg");
  background-attachment: fixed;
  background-size: cover;
  background-position: center center;
}

a:link,
a:visited {
  text-decoration: none;
  color: #f08c00;
}

h2 {
  background-color: #f08c00;
  color: #fff;
  text-align: center;
  margin: 0;
  padding: 20px;
  overflow: auto;
}
.listing {
  list-style: none;
  margin: 2em;
  display: grid;
  grid-gap: 20px;
  grid-template-rows: repeat(auto-fit, minmax(200px, 1fr));
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  padding-left: 0;
}
.listing li {
  border: 1px solid #ffe066;
  border-radius: 5px;
  display: flex;
  flex-direction: column;
}
.listing .cta {
  margin-top: auto;
  border-top: 1px solid #ffe066;
  padding: 10px;
  text-align: center;
}
.listing .body {
  padding: 10px;
}
</style>
