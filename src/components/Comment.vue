<template>
  <div class="container-fluid mt-4">
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <h3>Write a Comment</h3>
          <div class="input-group">
            <div class="input-group-prepend">
              <button @click.prevent="sendComment()" class="btn btn-primary">Send</button>
            </div>
            <textarea v-model="contentComment" class="form-control" aria-label="With textarea"></textarea>
          </div>
        </div>
        <div class="col-md-6">
          <h3>Comments</h3>
          <div v-for="comment in allComment" :key="comment.id" class="comment">
            <div class="text d-flex justify-content-between">
              <div>
                <span>{{comment.content}}</span>
                <br />
                <small class="timestamp">-> {{comment.timestamp | formatDate }}</small>
              </div>
            </div>
            <button @click.prevent="deleteComment(comment.id)" class="btn btn-danger">Delete</button>
          </div>
        </div>
      </div>
    </div>
    <!--{{for comment in comments}}-->
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  name: "comment",
  props: ["carId"],
  data() {
    return {
      contentComment: "",
      allComment: []
    };
  },
  methods: {
    getComments() {
      const path = "http://localhost:7070/api/v1.0/comments/";
      console.log(path);
      axios
        .get(path, {
          params: {
            car: this.carId
          }
        })
        .then(response => {
          console.log(response.data);
          this.allComment = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    sendComment() {
      const path = "http://localhost:7070/api/v1.0/comments/";
      console.log(path);
      axios
        .post(path, {
          car: this.carId,
          content: this.contentComment
        })
        .then(response => {
          this.getComments();
          console.log(response.data);
          this.contentComment = "";
        })
        .catch(error => {
          console.log(error);
        });
    },
    deleteComment(iD) {
      const path = "http://localhost:7070/api/v1.0/comments/";
      const fullpath = path + iD + "/";
      console.log(fullpath);
      axios
        .delete(fullpath)
        .then(() => {
          this.getComments();
          console.log("Borrado");
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  filters: {
    formatDate: function(value) {
      if (value) {
        return moment(String(value)).format("MM/DD/YYYY hh:mm");
      }
    }
  },
  created() {
    this.getComments();
  }
};
</script>

<style lang="css" scoped>
.comment {
  background-color:#f8f9fa;
  margin: 10px;
  vertical-align: center;
  padding: 10px;
  border-radius: 10px;
  overflow: -moz-hidden-unscrollable;
}
</style>