<template>
  <div id="app">
    <header class="header">
      <nav class="navbar navbar-expand-lg">
        <div class="container"><a href="/#/" class="navbar-brand"><img src="images/conveyNewWhiteBrdr.png" alt="logo" height="65" width="210" class="d-none d-lg-block"><img src="images/conveyNewWhiteBrdr.png" alt="logo" height="65" width="210" class="d-block d-lg-none"><span class="sr-only">Go to homepage</span></a>

          <div id="navbarSupportedContent" class="collapse navbar-collapse">
            <ul class="navbar-nav ml-auto">

              <li class="nav-item">
                <form v-on:submit.prevent="searchWord()" class="form-inline my-2 my-lg-0">
                  <input v-model="inputWord" class="form-control mr-sm-2" type="search" placeholder="Center me, widen me, and put me under the logo" aria-label="Search a word">
                  <button class="btn btn-outline-success my-2 my-sm-0" type="submit"><i class="fa fa-search"></i></button>
                </form>
              </li>

              <li class="nav-item"><a href="/#/createWords" class="nav-link">Create</a></li>

              <!-- DROPDOWN MENU -->
              <li class="nav-item dropdown"><a id="community" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" class="nav-link dropdown-toggle">Menu</a>
                <div aria-labelledby="community" class="dropdown-menu"><a href="/#/about" class="dropdown-item">About Us</a><a href="/#/signup" class="dropdown-item">Signup</a><a href="" class="dropdown-item">Explore</a><a href="" class="dropdown-item">Discuss</a><a href="" class="dropdown-item">Vote</a><a href="" class="dropdown-item">Community</a><a href="/#/signup" class="dropdown-item">Blog</a><a href="" class="dropdown-item">Library</a></div>
              </li>




              <!-- LOGIN MODAL -->
              <li class="nav-item dropdown"><a href="/#/login" data-toggle="modal" class="btn navbar-btn btn-outline-light mb-5 mb-lg-0"><i class="fa fa-sign-in"></i>Login</a></li>
            </ul>
          </div>
        </div>
      </nav>
    </header>

    <router-view/>

    <footer class="footer">
      <div class="footer__block">
        <div class="container">
          <div class="row">
            <div class="col-lg-4 col-md-12 mb-5">
              <h4 class="h5">About Jobs</h4>
              <p>Jobs is a <strong>Bootstrap 3 jobs board theme </strong> developed in the middle of Europe by <a href="http://ondrejsvestka.cz/">Ondrej Svestka</a></p>
              <p> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus magna. Cras in mi at felis aliquet congue. </p>
            </div>
            <div class="col-lg-4 col-md-6 mb-5">
              <h4 class="h5">This Theme</h4>
              <ul class="list-unstyled">
                <li><a href="index.html">Home</a></li>
                <li><a href="category.html">Jobs Listing</a></li>
                <li><a href="detail.html">Job detail</a></li>
                <li><a href="about.html">About</a></li>
                <li><a href="contact.html">Contact</a></li>
                <li><a href="blog.html">Blog listing</a></li>
                <li><a href="post.html">Blog Post</a></li>
                <li><a href="packages.html">Pricing packages</a></li>
                <li><a href="testimonials.html">Testimonials</a></li>
                <li><a href="text.html">Text page</a></li>
                <li><a href="faq.html">FAQ</a></li>
              </ul>
            </div>
            <div class="col-lg-4 col-md-6">
              <h4 class="h5">Our offices</h4>
              <h5>London</h5>
              <p> Donec eleifend<br />libero at sagittis<br />mollis + 44 2556 789 8799</p>
              <h5>Paris</h5>
              <p> Donec eleifend<br />libero at sagittis<br />mollis + 41 2556 789 8799</p>
            </div>
          </div>
          <div class="row">
            <div class="col-lg-4 col-md-6 mb-5">
              <h4 class="h5">Client zone</h4>
              <ul class="list-unstyled">
                <li><a href="client-register.html">Login or Register</a></li>
                <li><a href="client-dashboard.html">Dashboard</a></li>
                <li><a href="client-applicants.html">Applicants</a></li>
                <li><a href="client-job.html">Post a new job</a></li>
              </ul>
            </div>
            <div class="col-lg-4 col-md-6 mb-5">
              <h4 class="h5">Let's be Friends</h4>
              <p class="social"><a href="#" data-animate-hover="pulse" class="external facebook"><i class="fa fa-facebook"></i></a><a href="#" data-animate-hover="pulse" class="external gplus"><i class="fa fa-google-plus"></i></a><a href="#" data-animate-hover="pulse" class="external twitter"><i class="fa fa-twitter"></i></a><a href="#" data-animate-hover="pulse" class="email"><i class="fa fa-envelope"></i></a></p>
            </div>
            <div class="col-lg-4 col-md-12 mb-5">
              <h4 class="h5">News and Updates</h4>
              <p>Sign up to get weekly portion of fresh jobs and news from us.</p>
              <form class="footer__newsletter">
                <div class="input-group">
                  <input type="text" placeholder="Enter your email address" aria-describedby="emailAddress" class="form-control">
                  <div class="input-group-append">
                    <button id="emailAddress" type="button" class="btn btn-default input-group-text"><i class="fa fa-send"></i></button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
      <div class="footer__copyright">
        <div class="container">
          <div class="row">
            <div class="col-md-6 text-md-left text-center">
              <p>&copy;2017 Best company</p>
            </div>
            <div class="col-md-6 text-md-right text-center">
              <p class="credit">Theme by <a href="https://ondrejsvestka.cz/">Ondrej Svestka</a></p>
            </div>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<!-- <style>
</style> -->

<script>
export default {
  data: function() {
    return {
      inputWord: ""
    };
  },
  methods: {
    searchWord: function() {
      var url = "/?search=" + this.inputWord;
      this.inputWord = "";
      this.$router.push(url);
    }
  }
};


// import CommentsModal from "./components/CommentsModal.vue";
// import DefinitionsModal from "./components/DefinitionsModal.vue";
// var axios = require("axios");

// export default {
//   data: function() {
//     return {
//       words: [],
//       wordnikWords: [],
//       search: "",
//       i: 0
//     };
//   },
//   components: {
//     commentsModal: CommentsModal,
//     definitionsModal: DefinitionsModal
//   },
//   created: function() {
//     console.log("Finding your word.");
//   },
//   methods: {
//     searchEntry: function() {
//       console.log(this.search);
//       var params = {
//         search: this.search
//       };
//       console.log(params);
//       axios.get("http://localhost:3000/api/words", { params: params }).then(
//         function(response) {
//           console.table(response.data);
//           this.words = response.data.custom_words;
//           console.log("CONVEY WORDS", this.words);
//         }.bind(this)
//       );
//       axios.get("http://localhost:3000/api/wordnik", { params: params }).then(
//         function(response) {
//           // The response.data is an array of hashes
//           console.log("WORDNIK WORDS", response.data);
//           this.wordnikWords = response.data;
//         }.bind(this)
//       );
//     },
//     trimWords: function(wordnikWords) {
//       return wordnikWords.slice(0, 3);
//     },
//     createDefinition: function(word) {
//       var params = {
//         definition: word.newDefinition,
//         word_id: word.id
//       };
//       axios
//         .post("http://localhost:3000/api/definitions", params)
//         .then(function(response) {
//           var newDefinition = response.data;
//           console.log(newDefinition);
//           word.definitions.push(newDefinition);
//           word.newDefinition = "";
//         });
//     },
//     searchTag: function(tag) {
//       this.search = tag.name;
//       this.searchEntry();
//     }
//   },
//   computed: {}
// };
</script>
