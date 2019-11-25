<template>
  <div class="topics">{{results.length}}</div>
</template>

<script>
export default {
  name: "topics",
  props: {
    results: {
      type: Array,
      default: []
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
