<template>
  <div>
    <!-- Button trigger modal -->
    <button type="button" class="my-nav-searchbtn" data-toggle="modal" v-bind:data-target="htmlId">
      {{ name }}
    </button>

    <!-- Modal -->
    <div class="modal fade" v-bind:id="modalId" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">{{ name }}</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>

          <div class="modal-body">
            Total {{ modalId }}
            <div>

            <!-- New Comment Text Input Form -->
            <form>
              <textarea type="text" v-model="word.comment" placeholder="enter a comment"></textarea> 
              <button class="my-nav-searchbtn" v-on:click="createComment(word)" type="submit">Submit</button>
            </form>
            </div>

            <ol>
              <li v-for="comment in word.comments">
                <p>{{ comment.text }}</p>
              </li>
            </ol>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
var axios = require("axios");

export default {
  name: "CommentsModal",
  props: {
    wordId: Number,
    name: String,
    word: Object
  },
  data: function() {
    return {
      htmlId: "#" + this.name + "-" + this.wordId,
      modalId: this.name + "-" + this.wordId
    };
  },
  methods: {
    createComment: function(word) {
      var params = {
        text: word.comment,
        word_id: word.id
      };
      axios
        .post("http://localhost:3000/api/comments", params)
        .then(function(response) {
          var newComment = response.data;
          console.log(newComment);
          word.comments.push(newComment);
          word.comment = "";
        });
    }
  }
};
</script>
