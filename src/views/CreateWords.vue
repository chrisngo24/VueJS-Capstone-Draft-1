<template>
  <div class="create">
    <h1>Contribute to the Convey Library</h1>
      <form>
        New Word: <input class="word-name" type="text" placeholder=" word name" aria-label="Word" v-model="newWord.word">
        Definition: <input class="word-definition" type="text" placeholder=" what does it mean?" aria-label="Define" v-model="newWord.definition">
        Context Example: <input class="word-example" type="text" placeholder=" use it in a sentence" aria-label="Example" v-model="newWord.example">
        <!-- Tag It: <input class="word-tag" type="text" placeholder="   Add Tags of Related or Similar Words So Others Are Able to Find Your Addition to the Library!" aria-label="Tag" v-model="word-tag"> -->
        <h6>Please review thoroughly before making your submission.</h6>
        <button v-on:click="createNewWord()" type="submit">Submit My Word!</button>
      </form>

    <h3>You Created: {{ createdWord.word }}</h3>
      <p>Which you defined: {{ createdWord.definition }}</p>
      <p>Your Example: {{ createdWord.example }}</p>

  </div>
</template>

<style>
</style>

<script>
import axios from "axios";
// var axios = require("axios");

export default {
  data: function() {
    return {
      newWord: { word: "", definition: "", example: "" },
      createdWord: {}
    };
  },
  created: function() {
    console.log("Your word has been submitted to the Convey library.");
  },
  methods: {
    createNewWord: function() {
      var params = {
        word: this.newWord.word,
        definition: this.newWord.definition,
        example: this.newWord.example
      };
      axios.post("http://localhost:3000/api/words", params).then(
        function(response) {
          console.log(response.data);
          this.newWord = { word: "", definition: "", example: "" };
          this.createdWord = response.data;
        }.bind(this)
      );
    }
  },
  computed: {}
};
</script>
