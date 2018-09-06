<template>
  <div id="app">
    <header class="header">
      <nav class="navbar navbar-expand-lg">
        <div class="container"><a href="/" class="navbar-brand"><img src="images/CONVEY/logo-sans-white-blue-slash-thick.png" alt="logo" height="75" width="240" class="d-none d-lg-block"><img src="images/CONVEY/logo-sans-white-blue-slash-thick.png" alt="logo" height="75" width="240" class="d-block d-lg-none"><span class="sr-only">Go to homepage</span></a>

          <div id="navbarSupportedContent" class="collapse navbar-collapse">
            <ul class="navbar-nav ml-auto">

              <!-- NAVBAR SEARCHBAR -->
              <li class="nav-item">
                <form v-on:submit.prevent="searchWord()" class="form-inline my-2 my-lg-0">
                  <input v-model="inputWord" class="form-control mr-sm-2" id="my-search" type="search" placeholder="Type search here" aria-label="Search a word">
                  <button class="btn btn-outline-success my-2 my-sm-0 my-nav-searchbtn" type="submit"><i class="fa fa-search"></i></button>
                </form>
              </li>

              <li class="nav-item"><a href="/#/createWords" class="nav-link">Create</a></li>

              <!-- DROPDOWN MENU -->
              <li class="nav-item dropdown"><a id="community" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false" class="nav-link dropdown-toggle">Menu</a>
                <div aria-labelledby="community" class="dropdown-menu" id="my-dropdown-menu"><a href="/#/about" class="dropdown-item">About Us</a><a href="/#/signup" class="dropdown-item">Signup</a><a href="/#/login" class="dropdown-item">Login</a><a href="" class="dropdown-item">Explore</a><a href="" class="dropdown-item">Discuss</a><a href="" class="dropdown-item">Vote</a><a href="" class="dropdown-item">Community</a><a href="/#/signup" class="dropdown-item">Blog</a><a href="" class="dropdown-item">Library</a></div>
              </li>




              <!-- LOGIN MODAL -->
              <li class="nav-item dropdown" id="my-login-btn"><a href="#loginModal" data-toggle="modal" class="btn navbar-btn btn-outline-light mb-5 mb-lg-0" id="my-login-btn"><i class="fa fa-sign-in"></i>Login</a></li>
            </ul>
          </div>
        </div>
      </nav>
    </header>
    <!-- *** LOGIN MODAL ***_________________________________________________________
    -->
    <div id="loginModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true" class="modal fade">
      <div role="document" class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h4 id="exampleModalLabel" class="modal-title">Customer Login</h4>
            <button type="button" data-dismiss="modal" aria-label="Close" class="close"><span aria-hidden="true">×</span></button>
          </div>
          <div class="modal-body">
            <form v-on:submit.prevent="submit()" action="https://demo.bootstrapious.com/jobs/2-0-1/customer-orders.html" method="post">
              <div class="form-group">
                <input id="email_modal" type="text" placeholder="email" class="form-control" v-model="email">
              </div>
              <div class="form-group">
                <input id="password_modal" type="password" placeholder="password" class="form-control" v-model="password">
              </div>
              <p class="text-center">
                <button type="submit" class="btn btn-outline-white-primary"><i class="fa fa-sign-in"></i> Log in</button>
              </p>
            </form>
            <p class="text-center text-muted">Not registered yet?</p>
            <p class="text-center text-muted"><a href="client-register.html"><strong>Register now</strong></a>! It is easy and done in 1 minute and gives you access to special discounts and much more!</p>
          </div>
        </div>
      </div>
    </div>
    <!-- *** LOGIN MODAL END ***-->
    <router-view/>

    <footer class="footer">
      <div class="footer__block">
        <div class="container">
          <div class="row">
            <div class="col-lg-4 col-md-12 mb-5">
              <h4 class="h5">PAGES</h4>
              <ul class="list-unstyled">
                <p><a href="/" class="my-footer-links">Home</a></p>
                <p><a href="/#/about" class="my-footer-links">About</a></p>
                <p><a href="/#/createWords" class="my-footer-links">Create</a></p>
              </ul>
            </div>
            <div class="col-lg-4 col-md-6 mb-5">
              <h4 class="h5">FEATURES IN PROGRESS</h4>
                <p>Explore</p>
                <p>Discuss</p>
                <p>Vote</p>
                <p>Blog</p>
            </div>
            <div class="col-lg-4 col-md-6">
              <h4 class="h5">Built By Chris Ngo</h4>
              <h5>cngo2417@gmail.com</h5>
                <p><a href="https://www.linkedin.com/in/chrisngo24/" target="_blank">LinkedIn</a></p>
                <p><a href="https://github.com/chrisngo24/" target="_blank">Github</a></p>
                <p><a href="http://anyonecanlearntocode.com/" target="_blank">Actualize Coding Bootcamp</a></p>
            </div>
          </div>
          <a href="/#/" <img src="images/CONVEY/logo-sans-yellow-black-slash-thick.png" alt="logo" height="100" width="240" class="d-none d-lg-block"><img src="images/CONVEY/logo-sans-yellow-black-slash-thick.png" alt="logo" height="100" width="240" class="d-block d-lg-none"></a>
        </div>
      </div>
      <div class="footer__copyright">
        <div class="container">
          <div class="row">
            <div class="col-md-6 text-md-left text-center">
              <p>&copy;CONVEY</p>
              <p>Capstone 2018</p>
            </div>
            <div class="col-md-6 text-md-right text-center">
              <p class="credit">Made in Chicago</p>
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
import axios from "axios";
export default {
  data: function() {
    return {
      inputWord: "",
      email: "",
      password: "",
      errors: []
    };
  },
  methods: {
    searchWord: function() {
      var url = "/?search=" + this.inputWord;
      this.inputWord = "";
      this.$router.push(url);
    },
    submit: function() {
      var params = {
        email: this.email,
        password: this.password
      };
      axios
        .post("http://localhost:3000/api/sessions", params)
        .then(response => {
          axios.defaults.headers.common["Authorization"] =
            "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          this.$router.push("/");
          $("#loginModal").modal("hide");
        })
        .catch(error => {
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
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
