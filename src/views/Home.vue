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

    <hr>
    <!-- SEARCH RESULTS DISPLAY -->
    <section lass="bg-light-gray">
      <div class="container">
        <div class="row">
          <div id="blog-post" class="col-lg-10 mx-auto">
            <div id="post-content">
              <h2>Established Definitions for "{{ search }}"</h2>
              <h6>[Officially sourced from the Wordnik Dictionary]</h6>
            
              <ol>
                <li v-for="wordnikWord in trimWords(wordnikWords)">
                  <p>{{ wordnikWord.word }}</p>
                  <p>Definition: {{ wordnikWord.text }}</p>
                </li>
              </ol>
            
            <hr>

            <section>
              <h2>Convey Definitions for "{{ search }}"</h2>
              <h6>[Created by Convey users]</h6>
                <p v-if="words.length === 0">The word you are looking for does not yet exist in the Convey library. If you can define it, consider adding it to the library.</p>

                  <ol>
                    <li v-for="word in words">
                      <p class="word"><h6>{{ word.word }}</h6></p>
                      <p class="definition">Definition: {{ word.definition }}</p>
                      <p class="example">Example: {{ word.example }}</p>
                      <p class="user-name">Conveyed By: <a href="#">{{ word.user_id }}</a></p>
                      
                      <p class="tags">Tags:
                          <span v-for="tag in word.tags">
                            <button v-on:click="searchTag(tag)">{{ tag.name }}</button>
                          </span>

                      <commentsModal v-bind:wordId="word.id" name="Comments" :word="word"></commentsModal>
                     
                      <definitionsModal v-bind:wordId="word.id" name="Redefine It" :word="word"></definitionsModal>

                      <h4>DEFINITIONS BY OTHER CONVEY USERS</h4>
                      <p>
                        <ol>
                          <li v-for="definition in word.definitions">
                            <p><a href="#">{{ word.word }}</a></p>
                            <p>Definition: {{ definition.definition }}</p>
                            <p>Example: {{ definition.example }}</p>
                            <p>Conveyed By: <a href="#">{{ definition.user_id }}</a></p>
                          </li>
                        </ol>
                      </p>
                      
                    </li>
                  </ol>
            </section>
              <blockquote class="blockquote">
                <p><!-- Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus magna. Cras in mi at felis aliquet congue. Ut a est eget ligula molestie gravida. Curabitur massa. Donec eleifend, libero at sagittis mollis, tellus est malesuada tellus, at luctus turpis elit sit amet quam. Vivamus pretium ornare est. --></p>
              </blockquote>
              <h3><!-- Header Level 3 --></h3>
              <p><!-- Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo. Quisque sit amet est et sapien ullamcorper pharetra. Vestibulum erat wisi, condimentum sed, commodo vitae, ornare sit amet, wisi. Aenean fermentum, elit eget tincidunt condimentum, eros ipsum rutrum orci, sagittis tempus lacus enim ac dui. Donec non enim in turpis pulvinar facilisis. Ut felis. Praesent dapibus, neque id cursus faucibus, tortor neque egestas augue, eu vulputate magna eros eu erat. Aliquam erat volutpat. Nam dui mi, tincidunt quis, accumsan porttitor, facilisis luctus, metus --></p>
              <ul>
                <li><!-- Lorem ipsum dolor sit amet, consectetuer adipiscing elit. --></li>
                <li><!-- Aliquam tincidunt mauris eu risus. --></li>
              </ul>
              <p><!-- <img src="https://d19m59y37dris4.cloudfront.net/jobs/2-0-1/img/blog1.jpg" alt="Example blog post alt" class="img-fluid"> --></p>
              <p><!-- Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo. Quisque sit amet est et sapien ullamcorper pharetra. Vestibulum erat wisi, condimentum sed, commodo vitae, ornare sit amet, wisi. Aenean fermentum, elit eget tincidunt condimentum, eros ipsum rutrum orci, sagittis tempus lacus enim ac dui. Donec non enim in turpis pulvinar facilisis. Ut felis. Praesent dapibus, neque id cursus faucibus, tortor neque egestas augue, eu vulputate magna eros eu erat. Aliquam erat volutpat. Nam dui mi, tincidunt quis, accumsan porttitor, facilisis luctus, metus --></p>
            </div>
            <!-- /#post-content-->
            <!-- <div id="comments"> -->
              <!-- <h4>2 comments</h4>
              <div class="row comment">
                <div class="col-sm-3 col-md-2 text-center-xs">
                  <p><img src="https://d19m59y37dris4.cloudfront.net/jobs/2-0-1/img/blog-avatar2.jpg" alt="" class="img-fluid rounded-circle"></p>
                </div>
                <div class="col-sm-9 col-md-10">
                  <h5>Julie Alma</h5>
                  <p class="posted"><i class="fa fa-clock-o"></i> September 23, 2011 at 12:00 am</p>
                  <p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo.</p>
                  <p class="reply"><a href="#"><i class="fa fa-reply"></i> Reply</a></p>
                </div>
              </div> -->
              <!-- /.comment-->
              <!-- <div class="row comment last">
                <div class="col-sm-3 col-md-2 text-center-xs">
                  <p><img src="https://d19m59y37dris4.cloudfront.net/jobs/2-0-1/img/blog-avatar.jpg" alt="" class="img-fluid rounded-circle"></p>
                </div>
                <div class="col-sm-9 col-md-10">
                  <h5>Louise Armero</h5>
                  <p class="posted"><i class="fa fa-clock-o"></i> September 23, 2012 at 12:00 am</p>
                  <p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo.</p>
                  <p class="reply"><a href="#"><i class="fa fa-reply"></i> Reply</a></p>
                </div> -->
              <!-- </div> -->
              <!-- /.comment-->
            <!-- </div> -->
            <!-- /#comments-->
            <!-- <div id="comment-form">
              <h4>Leave comment</h4>
              <form>
                <div class="row">
                  <div class="col-md-6">
                    <div class="form-group">
                      <label for="name">Name <span class="required">*</span></label>
                      <input id="name" type="text" class="form-control">
                    </div>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-6">
                    <div class="form-group">
                      <label for="email">Email <span class="required">*</span></label>
                      <input id="email" type="text" class="form-control">
                    </div>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-12">
                    <div class="form-group">
                      <label for="comment">Comment <span class="required">*</span></label>
                      <textarea id="comment" rows="4" class="form-control"></textarea>
                    </div>
                  </div>
                </div>
                <div class="row">
                  <div class="col-md-12 text-right">
                    <button type="button" class="btn btn-outline-white-primary"><i class="fa fa-comment-o"></i> Post comment</button>
                  </div>
                </div>
              </form> -->
            <!-- </div> -->
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
