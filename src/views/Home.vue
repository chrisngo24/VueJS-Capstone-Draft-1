<template>
  <div class="home">
    <div>
      <h1 class="title">CONVEY</h1>
    </div>
 
    <div class="subtitle">
      <h6>It's time we have better conversations.</h6>
    </div>
      <div class="pages-links">
        <h6> [ Dictionary ] . [ Thesaurus ] . [ Urban Dictionary ] . [ Origin & History ] . [ Create ] . [ Blog ] . [ Vote/Discuss ] </h6>
      </div>
        <div class="search-bar">
          <h3><input v-on:keyup.enter="submit" class="search-box" type="text" v-model="search"></h3>
          <button class="search-button" v-on:click="searchEntry()">Convey</button>
        </div>


    <div class="results-body">
      <h5>Your search results: {{ search }}</h5> 
        <p v-if="words.length === 0">The word you are looking for does not yet exist with Convey.</p>
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
  padding-bottom: 40px;
}
.pages-links {
  font-size: 20;
  color: black;
  text-align: center;
  padding-bottom: 30px;
}
.search-bar {
  color: black;
  text-align: center;
  padding-top: 20px;
}
.search-box {
  height: 39px;
  width: 37%;
  border-style: solid;
  border-width: 1px;
  border-radius: 17px;
}
.search-button {
  height: 35px;
  width: 10%;
  background-color: black;
  color: white;
  font-size: 20px;
  font-weight: bold;
  border-radius: 17px;
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2), 0 6px 5px 0 rgba(0,0,0,0.19);
}
.search-button:hover {
  background-color: white;
  color: black;
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
      axios.get("http://localhost:3000/api/words", {params: params}).then(
        function(response) {
          console.table(response.data);
          this.words = response.data;
        }.bind(this)
      );
    },
    // press enter to submit: function() {

    // }
  },
  computed: {}
};
</script>
