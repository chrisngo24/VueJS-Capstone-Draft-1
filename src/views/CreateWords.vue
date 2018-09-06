<template>
  <section>
    <div class="container">
        <div class="row">
          <div class="col-lg-10 mx-auto">
            <form id="job-main-form" method="get" action="#" class="job-add-form">
              <div class="row">
                <div class="col-lg-12">
                  <h2>ADD TO OUR DICTIONARY</h2>
                  <h5 class="account-required-warning">You must be registered and logged in, in order to make a submission so we can validate your content and maintain a proper community.</h5>
                  <h6 class="input-required-warning">Input is required for all fields marked with *</h6>
                  <hr>
                </div>
              </div>
              <div class="col-lg-12 form-group">
                <label for="title">New Word/Phrase*</label>
                <input id="title" type="text" class="form-control" v-model="newWord.word">
                <p class="text-muted text-small">If you are looking to add a different definition to a word that we already have in our dictionary, please search for the word instead, then just click on the "Redefine" button underneath the first definition. Please continue on if you are creating a new word with different spelling, punctuation or any other additions.     </p>
              </div>
              <div class="row">
                <div class="col-lg-12 form-group">
                  <label for="text">Definition of Your Word*</label>
                  <textarea id="text" rows="5" class="form-control" v-model="newWord.definition"></textarea>
                  <p class="help-block text-small">Be clear.</p>
                </div>
              </div>
              <div class="row">
                <div class="col-lg-12 form-group">
                  <label for="text">Example*</label>
                  <textarea id="text" rows="1" class="form-control" v-model="newWord.example"></textarea>
                  <p class="help-block text-small">What's the most common usage context for your particular definition of the word? Use the word or phrase in a sentence or paragraph if you need to. Most importantly, provide contextual details where necessary.</p>
                </div>
              </div>
              <div class="row">
                <div class="col-lg-12 form-group">
                  <label for="tag">Tag It*</label>
                  <textarea id="tag" rows="1" class="form-control" placeholder="coding, student, cat, dog, artist, sport, etc." v-model="newWord.wordtag"></textarea>
                  <p class="help-block text-small">Give it tags to similar or related words so others can use it to learn and lead to better understanding. Keep in mind, users may be looking for alternatives to your word.</p>
                </div>
              </div>
              <div class="row">
                <div class="col-lg-4 form-group">
                  <label for="company_logo">Images</label>
                  <input id="company_logo" type="file" class="form-control">
                  <p class="help-block text-small">Provide visual representation with an image, photo or gif.</p>                  
                </div>
                <div class="col-lg-4 form-group">
                  <label for="company_logo">Video</label>
                  <input id="company_logo" type="file" class="form-control">
                  <p class="help-block text-small">Upload a short video clip to define your word/phrase.</p> 
                </div>
                <div class="col-lg-4 form-group">
                  <label for="company_logo">Audio</label>
                  <input id="company_logo" type="file" class="form-control">
                  <p class="help-block text-small">Express your word/phrase with audio. How do you pronounce it, use it?, etc.</p> 
                </div>                
              </div>
              <div class="row">
                <div class="col-lg-12 text-center">
                  <router-link :to="{name: 'home'}">
                    <button v-on:click="createNewWord()" type="submit" id="my-main-search-btn"> <i class="fa fa-magic"></i> Submit to CONVEY Dictionary</button>
                  </router-link>
                  <p class="help-block text-small">Please review your entire post for accuracy, grammar, and punctuation before submitting.</p>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
  </section>
</template>

<script>
import axios from "axios";
// var axios = require("axios");

export default {
  data: function() {
    return {
      newWord: { word: "", definition: "", example: "", wordtag: "" },
      createdWord: {}
    };
  },
  created: function() {
    console.log("Your word has been added to the Convey library.");
  },
  methods: {
    createNewWord: function() {
      var params = {
        word: this.newWord.word,
        definition: this.newWord.definition,
        example: this.newWord.example,
        tags: this.newWord.wordtag.split(", ")
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
