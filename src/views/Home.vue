<template>
  <div class="home">
    <div>
      <h1 class="title">CONVEY</h1>
    </div>
 
    <div class="subtitle">
      <h6>It's time we have better conversations.</h6>
    </div>

      <div class="pages-links">
        <button type="button" class="btn-pages-links-tab">Dictionary</button>
        <button type="button" class="btn-pages-links-tab">Thesaurus</button>
        <button type="button" class="btn-pages-links-tab">Urban Dictionary</button>
        <button type="button" class="btn-pages-links-tab">History</button>
        <button type="button" class="btn-pages-links-tab">Create</button>
        <button type="button" class="btn-pages-links-tab">Discuss</button>
        <button type="button" class="btn-pages-links-tab">Vote</button>
      </div>
        <form class="form-center">
          <input class="search-form" type="search" placeholder="   Search" aria-label="Search" v-model="search">
          <button class="search-button" v-on:click="searchEntry()" type="submit">Search</button>
        </form>

    <div class="results-body">
      <h5>Your search results: {{ search }}</h5> 
        <p v-if="words.length === 0">The word you are looking for does not yet exist in the Convey library. If you can define it, consider adding it to the library.</p>
        <ul>
          <li v-for="word in words">
            <p class="word"><h3>Word: {{ word.word }}</h3></p>
            <p class="definition">Definition: <h5>{{ word.definition }}</h5></p>
            <p class="user-name">By User: <h6>{{ word.user_id }}</h6></p>
          </li>
        </ul> 
    </div> 
  </div>
</template>

<style>
.title {
  font-size: 45px;
  font-weight: bold;
  color: black;
  text-align: center;
}
.subtitle {
  font-variant: small-caps;
  color: black;
  text-align: center;
  padding-bottom: 15px;
}
.pages-links {
  font-size: 20;
  color: black;
  text-align: center;
  padding-bottom: 70px;
}
.btn-pages-links-tab {
  border-top: 0px white;
  border-right: 1px solid black;
  border-bottom: 0px white;
  border-left: 1px solid black;
  background-color: white;
}
.form-inline {
  color: black;
  text-align: center;
  padding-top: 30px;
}
.search-form {
  height: 39px;
  width: 38%;
  border-top: 0px white;
  border-right: 0px white;
  border-bottom: 1.5px solid black;
  border-left: 0px white;
  background-color: white;
  border-radius: 11px;
  margin-bottom: 4px;
}
.search-button {
  padding-top: 3px;
  height: 39px;
  width: 9%;
  background-color: white;
  color: black;
  font-size: 20px;
  font-weight: bold;
  border-top: 1.5px solid black;
  border-right: 0px white;
  border-bottom: 0px white;
  border-left: 0px white;
  border-style: solid;
  border-radius: 11px;
  /*box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 5px 0 rgba(0, 0, 0, 0.19);*/
}
.search-button:hover {
  background-color: black;
  color: white;
}
.results-body {
  text-align: left;
  padding-top: 50px;
  padding-left: 100px;
  padding-right: 100px;
  padding-bottom: 50px;
}
.word {
  font-weight: bold;
  font-size: 22px;
  padding-top: 30px;
  padding-left: 7px;
}
.definition {
  padding-top: 7px;
  padding-left: 7px;
}
.user-name {
  padding-top: 7px;
  padding-left: 7px;
}
</style>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      words: [{ id: "", word: "", definition: "", user_id: "" }],
      search: "",
      message: "Chris was here"
    };
  },
  created: function() {
    console.log("Finding your word.");
  },
  methods: {
    searchEntry: function() {
      var params = {
        search: this.search
      };
      console.log(params);
      axios.get("http://localhost:3000/api/words", { params: params }).then(
        function(response) {
          console.table(response.data);
          this.words = response.data;
        }.bind(this)
      );
    }
    // press enter to submit: function() {
    // }
  },
  computed: {}
};
</script>
