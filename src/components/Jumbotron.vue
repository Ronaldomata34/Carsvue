<template>
  <div class="jumbotron">
    <div class="container">
      <h1 class="display-4">{{title}}</h1>

      <hr class="my-4" />
      <p></p>
      <div class="d-flex justify-content-between">
        <router-link class="btn btn-primary" :to="{ name: pathTo}">{{titleButton}}</router-link>
        <a
          target="blank"
          href="https://pdfhost.io/v/+ikVsWz7z_Scan1655pdf.pdf"
          class="btn btn-success"
        >View PDF</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Jumbotron",
  props: {
    title: String,
    titleButton: String,
    pathTo: String
  }
};
</script>

<style lang="css" scoped>
.jumbotron {
  color: white;
  border-radius: 0;
  background: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url("../assets/img/jumbotron-img-cars.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
</style>