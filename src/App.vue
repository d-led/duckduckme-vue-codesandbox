<template>
  <b-container id="app text-left">
    <h2>DuckDuckGo Graph Search</h2>
    <b-input-group>
      <b-form-input v-model="term" type="search" v-on:keydown="search"/>
      <b-input-group-append>
        <b-button @click="search">Search</b-button>
      </b-input-group-append>
    </b-input-group>
    <search-results :results="results" :error="error"></search-results>
  </b-container>
</template>

<script>
import SearchResults from "./components/SearchResults";
import axios from "axios";
import jsonpAdapter from "axios-jsonp";

export default {
  name: "App",
  components: {
    SearchResults
  },
  data() {
    return {
      term: "",
      results: [],
      error: null
    };
  },
  methods: {
    search: function(event) {
      if (event.key && event.key !== "Enter") {
        return;
      }
      axios({
        url: `https://api.duckduckgo.com/?q=${encodeURIComponent(
          this.term
        )}&format=json&pretty=1`,
        adapter: jsonpAdapter
      })
        .then(res => {
          this.error = null;
          this.results = res.data.RelatedTopics;
          if (this.results.length === 0) {
            this.error = "Nothing found ...";
          }
        })
        .catch(e => {
          this.error = e.message;
        });
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
