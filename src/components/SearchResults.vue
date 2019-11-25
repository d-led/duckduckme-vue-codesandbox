<template>
  <div>
    <h2 v-if="results.length > 0">Search Results</h2>
    <topics :results="results"></topics>

    <h2 v-if="results.length > 0">Related Topics</h2>
    <div v-for="result in results" class="result">
      <div v-if="result.Name">
        <h3>{{result.Name}}</h3>
        <topics :results="result.Topics"></topics>
      </div>
    </div>
  </div>
</template>

<script>
import Topics from "./Topics";

export default {
  name: "search-results",
  components: {
    Topics
  },
  props: {
    results: {
      type: Array,
      default: ()=>[]
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
