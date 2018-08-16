<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ testMessage }}</h2>
  </div>
</template>

<style>
</style>

<script>
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      testMessage: "This is a test."
    };
  },
  created: function() {},
  methods: {},
  computed: {}
};
</script>
