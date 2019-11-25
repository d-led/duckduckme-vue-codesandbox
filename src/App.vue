<template>
  <b-container id="app text-left">
    <h2>DuckDuckGo Graph Search</h2>
    <b-input-group>
      <b-form-input v-model="term" type="search" v-on:keydown="search"/>
      <b-input-group-append>
        <b-button @click="search">Search</b-button>
      </b-input-group-append>
    </b-input-group>
    <topics :results="results"></topics>

    <h2 v-if="results.length > 0">Search Results</h2>

    <div v-for="result in results" class="result">
      <ul>
        <div v-if="result.FirstURL">
          <li>
            <a :href="result.FirstURL">
              <p class="text-left">{{result.Text}}</p>
            </a>
          </li>
        </div>
      </ul>
    </div>
    <h2 v-if="results.length > 0">Related Topics</h2>
    <div v-for="result in results" class="result">
      <div v-if="result.Name">
        <h3>{{result.Name}}</h3>
      </div>
    </div>
  </b-container>
</template>

<script>
import Topics from "./components/Topics";
import axios from "axios";
import jsonpAdapter from "axios-jsonp";

export default {
  name: "App",
  components: {
    Topics
  },
  data() {
    return {
      term: "",
      results: []
    };
  },
  methods: {
    search: function(event) {
      if (event.key !== "Enter") {
        return;
      }
      axios({
        url: `https://api.duckduckgo.com/?q=${encodeURIComponent(
          this.term
        )}&format=json&pretty=1`,
        adapter: jsonpAdapter
      })
        .then(res => {
          this.results = res.data.RelatedTopics;
        })
        .catch(e => console.log(JSON.stringify(e)));
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
