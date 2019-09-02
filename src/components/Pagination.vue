<template>
  <div id="displayedListingsCount" class="d-flex justify-content-start">
    <div class="p-2">
      <button v-if="info.previous" class="btn btn-primary btn-sm" @click="getPreviousURL()">Previous</button>
    </div>
    <div class="p-2">
      <strong>{{currentPage}} - {{info.total_pages}} number of pages | {{info.count}} listings</strong> 
    </div>

    <div class="p-2">
      <button v-if="info.next" class="btn btn-primary btn-sm" @click="getNextURL()">Next</button>
    </div>
    <hr style="margin-bottom:50px" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Pagination",
  props: {
    info: Object
  },
  data() {
    return {
      page: 1,
      pageSize: 15,
      currentPage: 1,
      totalPages: "dsd",
      numberOfPages: ""
    };
  },
  methods: {
    getNextURL() {
      const path = this.info.next;
      axios
        .get(path)
        .then(response => {
          console.log(response.data);
          this.$emit("nextData", response.data);
          this.currentPage++;
        })
        .catch(error => {
          console.log(error);
        });
    },
    getPreviousURL() {
      const path = this.info.previous;
      axios
        .get(path)
        .then(response => {
          console.log(response.data);
          this.$emit("nextData", response.data);
          this.currentPage--;
        })
        .catch(error => {
          console.log(error);
        });
    }
    /*async getNextURL() {
      let data = await axios.get(this.info.next);
      this.numberOfPages = Math.ceil(this.info.count / this.pageSize);
      this.currentPage++;
      this.$store.commit("addListCarSection", data.data);
    },*/
    /*async getPreviousURL() {
      let data = await axios.get(this.info.previous);
      this.currentPage--;
      this.$store.commit("addListCarSection", data.data);
    }*/
  }
};
</script>

<style lang="css">
#displayedListingsCount {
    width: 500px;
}
</style>