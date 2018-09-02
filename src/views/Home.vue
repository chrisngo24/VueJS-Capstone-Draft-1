<template>
  <div class="home">
    <!-- SEARCH FORM -->
    <section class="job-form-section job-form-section--image">
      <div class="container">
        <div class="row">
          <div class="col-lg-8 mx-auto">
            <div class="job-form-box">
              <h2 class="heading">Find a <span class="accent">word</span> or <span class="accent">phrase</span>.</h2>
              <form  v-on:submit.prevent="searchEntry()" id="job-main-form" class="job-main-form">
                <div class="controls">
                  <div class="row align-items-center">
                    <div class="col-md-10">
                      <div class="form-group">
                        <label for="profession">Convey</label>
                        <input type="text" id="profession" name="profession" placeholder="Type search here" class="form-control" v-model="search">
                      </div>
                    </div>

                    <div class="col-md-2">
                      <button class="btn btn-outline-white-primary job-main-form__button" type="submit"><i class="fa fa-search"></i></button>
                    </div>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section>
      <h4>By Wordnik</h4>
      <div v-for="wordnikWord in trimWords(wordnikWords)">
        <ol>
          <li>
            <p class="word"><h6>Word: {{ wordnikWord.word }}</h6></p>
            <p class="word"><h6>Definition: {{ wordnikWord.text }}</h6></p>
          </li>
        </ol>
      </div>
        
      <hr>

      <h4>By the Community</h4>
      <p v-if="words.length === 0">The word you are looking for does not yet exist in the Convey library. If you can define it, consider adding it to the library.</p>
      <ol>
        <li v-for="word in words">
          <p class="word"><h6>{{ word.word }}</h6></p>
          <p class="definition">Definition: {{ word.definition }}</p>
          <p class="definition">Other User Definitions:
            <ul>
              <li v-for="definition in word.definitions">
                <p>{{ definition.definition }}</p>
              </li>
            </ul>
          </p>
          <p class="example">Example: {{ word.example }}</p>
          <p class="user-name">Conveyed By: {{ word.user_id }}</p>
          
          <p class="tags">Related Words:
              <span v-for="tag in word.tags">
                <button v-on:click="searchTag(tag)">{{ tag.name }}</button>
              </span>
          </p>
          
          <commentsModal v-bind:wordId="word.id" name="ShowComments" :word="word"></commentsModal> // ASK ABOUT THIS NAME CONNECTION THAT IS MESSING UP THE MODAL BUTTON IF YOU HAVE A SPACE BETWEEN WORDS//
         
          <definitionsModal v-bind:wordId="word.id" name="Definitions" :word="word"></definitionsModal>

        </li>
      </ol> 
    </section>
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
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2), 0 6px 5px 0 rgba(0, 0, 0, 0.19);
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
  font-style: italic;
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
import CommentsModal from "../components/CommentsModal.vue";
import DefinitionsModal from "../components/DefinitionsModal.vue";
var axios = require("axios");

export default {
  data: function() {
    return {
      words: [],
      wordnikWords: [],
      search: "",
      i: 0
    };
  },
  components: {
    commentsModal: CommentsModal,
    definitionsModal: DefinitionsModal
  },
  created: function() {
    console.log("Finding your word.", this.$route.query);
    if (this.$route.query.search) {
      this.search = this.$route.query.search;
      this.searchEntry();
    }
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
          this.words = response.data.custom_words;
          console.log("CONVEY WORDS", this.words);
        }.bind(this)
      );
      axios.get("http://localhost:3000/api/wordnik", { params: params }).then(
        function(response) {
          // The response.data is an array of hashes
          console.log("WORDNIK WORDS", response.data);
          this.wordnikWords = response.data;
        }.bind(this)
      );

      window.scrollTo(0, 0);
      
    },
    trimWords: function(wordnikWords) {
      return wordnikWords.slice(0, 3);
    },
    createDefinition: function(word) {
      var params = {
        definition: word.newDefinition,
        word_id: word.id
      };
      axios
        .post("http://localhost:3000/api/definitions", params)
        .then(function(response) {
          var newDefinition = response.data;
          console.log(newDefinition);
          word.definitions.push(newDefinition);
          word.newDefinition = "";
        });
    },
    searchTag: function(tag) {
      this.search = tag.name;
      this.searchEntry();
    }
  },
  computed: {}
};
</script>
