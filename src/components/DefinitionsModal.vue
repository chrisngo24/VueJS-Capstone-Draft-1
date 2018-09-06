<template>
  <div>
    <!-- Button trigger modal -->
    <button type="button" class="my-nav-searchbtn" data-toggle="modal" v-bind:data-target="htmlId">
      {{ displayName }}
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
<!--           <div class="modal-body">
            Total Definitions: {{ modalId }}
          </div> -->
         
          <div>
            <form>
              <textarea type="text" v-model="word.newDefinition" placeholder="enter a new definition"></textarea>
              <button class="my-nav-searchbtn" v-on:click="createDefinition(word)" type="submit">Submit</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
var axios = require("axios");

export default {
  name: "DefinitionsModal",
  props: {
    wordId: Number,
    name: String,
    displayName: String,
    word: Object
  },
  data: function() {
    return {
      htmlId: "#" + this.name + "-" + this.wordId,
      modalId: this.name + "-" + this.wordId
    };
  },
  methods: {
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
    }
  }
};
</script>
