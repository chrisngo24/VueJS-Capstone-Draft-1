<template>
  <div class="home">
    <div>
      <h1>Welcome to Capstone!</h1>
        <h6>Document, create, discuss & learn about the history and current evolution of language & communication.</h6>
    </div>

    <div class="search">
      <div>
        <h4>Start here</h4>
        <input type="text" v-model="searchBar">
        <button v-on:click="searchEntry(word)">Search</button>
      </div>
    </div>
  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      searchBar: "",
      searchEntry: "Route SHOW search entry to Wordnik API for data."
    };
  },
  created: function() {},
  methods: {
    searchEntry: function(word) {

    }
  },
  computed: {}
};
</script>
