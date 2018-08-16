<template>
  <div class="home">
    <h1>Welcome to Redef.com</h1>
      <h4>Document, create, discuss & learn about the history and current evolution of language & communication.</h4>

    <div class="search">
      <h2>Start with a word search here.</h2>
      <input type="text" v-model="searchBar">
      <button v-on:click="searchEntry()">Enter to search</button>
    </div>

  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      searchBar: "Search",
      searchEntry: "Route SHOW search entry to Wordnik API for data."
    };
  },
  created: function() {},
  methods: {},
  computed: {}
};
</script>
