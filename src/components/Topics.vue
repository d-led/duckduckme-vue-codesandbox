<template>
<div>
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
</div>
</template>

<script>
export default {
  name: "topics",
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
