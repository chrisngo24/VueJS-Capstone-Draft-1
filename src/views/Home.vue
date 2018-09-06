<template>
  <div class="home">
    <!-- SEARCH FORM -->
    <section class="job-form-section job-form-section--image">
      <div class="container">
        <div class="row">
          <div class="col-lg-10 mx-auto">
            <div class="job-form-box">
                <h2 class="heading">Inform the conversation.</h2>
              <form  v-on:submit.prevent="searchEntry()" id="job-main-form" class="job-main-form">
                <div class="controls">
                  <div class="row align-items-center">
                    <div class="col-md-10">
                      <div class="form-group">
                        <label for="profession"></label>
                        <input type="text" id="my-main-search-form" name="profession" placeholder="Type search here" class="form-control" v-model="search">
                      </div>
                    </div>

                    <div class="col-md-2">
                      <div class="form-group">
                        <button class="btn btn-outline-white-primary job-main-form__button" id="my-main-search-btn" type="submit"><i class="fa fa-search"></i></button>
                      </div>
                    </div>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- SEARCH RESULTS DISPLAY -->
    <section class="my-results-display">
      <div class="container">
        <div class="row">
          <div id="blog-post" class="col-lg-9 mx-auto">
            <div id="post-content">
              <h5><i>Search Results for "{{ search }}"</i></h5>

              <h2 class="wordnik-established-dictionary">The Established Dictionary</h2>
              <h6 class="provided-by-wordnik">Provided the Wordnik Dictionary</h6>
            
              <ol>
                <li v-for="wordnikWord in trimWords(wordnikWords)">
                  <p>{{ wordnikWord.word }}</p>
                  <p>Definition: {{ wordnikWord.text }}</p>
                </li>
              </ol>
            
            <hr>
            <hr>
            <hr>

            <section>
              <h2 class="convey-dictionary">The CONVEY Dictionary</h2>
              <h6 class="source-convey-users">By Convey Users</h6>
                <!-- <p v-if="words.length === 0">The word you are looking for does not yet exist in the Convey library. If you can define it, consider adding it to the library.</p> -->
                <p>{{ noWordsFoundMessage }}</p>

                  <ol>
                    <li v-for="word in words">
                      <p>{{ word.word }}</p>
                      <p>Definition: {{ word.definition }}</p>
                      <p>Example: "{{ word.example }}"</p>
                      <p>Conveyed By: <a href="#">{{ word.user.first_name + " " + word.last_name }}</a></p>
                      
                      <p class="tags">Tags:
                          <span v-for="tag in word.tags">
                            <button v-on:click="searchTag(tag)">{{ tag.name }}</button>
                          </span>

                      <commentsModal v-bind:wordId="word.id" name="Comments" :word="word"></commentsModal>
                     
                      <definitionsModal v-bind:wordId="word.id" name="Redefine" displayName="Redefine that thing" :word="word"></definitionsModal>
                      
                      <hr>
                      <hr>

                      <h4 class="convey-dictionary">DEFINITIONS BY OTHER CONVEYERS</h4>
                      <p>
                        <ol>
                          <li v-for="definition in word.definitions">
                            <p><a href="#">{{ word.word }}</a></p>
                            <p>Definition: {{ definition.definition }}</p>
                            <p>Example: "{{ definition.example }}"</p>
                            <p>Conveyed By: <a href="#">{{ definition.user.first_name + " " + definition.user.last_name }}</a></p>
                          </li>
                        </ol>
                      </p>
                    </li>
                  </ol>
            </section>
            </div> 
          </div>
        </div>
      </div>
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
import Vue from "vue";
import CommentsModal from "../components/CommentsModal.vue";
import DefinitionsModal from "../components/DefinitionsModal.vue";
var axios = require("axios");

export default {
  data: function() {
    return {
      words: [],
      wordnikWords: [],
      search: "",
      noWordsFoundMessage: "",
      i: 0
    };
  },
  components: {
    commentsModal: CommentsModal,
    definitionsModal: DefinitionsModal
  },
  create: function() {
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

          if (this.words.length === 0) {
            this.noWordsFoundMessage =
              "The word you are looking for does not yet exist in the Convey library. If you can define it, consider adding it to the library.";
          } else {
            this.noWordsFoundMessage = "";
          }
          console.log("CONVEY WORDS", this.words);
          this.search = "";
        }.bind(this)
      );
      axios.get("http://localhost:3000/api/wordnik", { params: params }).then(
        function(response) {
          // The response.data is an array of hashes
          console.log("WORDNIK WORDS", response.data);
          this.wordnikWords = response.data;

          Vue.nextTick(function() {
            document.querySelector("#blog-post").scrollIntoView({
              block: "start",
              inline: "nearest",
              behavior: "smooth"
            });
          });
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
