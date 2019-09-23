<template>
  <div>
    <NavBar></NavBar>
    <Jumbotron title="Web Car Scraper" pathTo="cars" titleButton="Search Cars"></Jumbotron>
    <div class="container">
      <h1 class="mb-4">Details</h1>
      <div class="row no-gutters">
        <div class="col-md-4">
          <img v-if="car.main_picture" :src="car.main_picture" class="card-img" alt />
          <img
            v-else
            src="https://static1.cargurus.com/gfx/cg/noImageAvailable_large.png"
            class="card-img"
            alt
          />
        </div>
        <div class="col-md-8">
          <div class="card-body">
            <div class="row">
              <div class="col-md-6">
                <strong>Make:</strong>
                {{car.make}}
              </div>
              <div class="col-md-6">
                <strong>Model:</strong>
                {{car.model.name}}
              </div>
              <div class="col-md-6">
                <strong>Year:</strong>
                {{car.year}}
              </div>
              <div class="col-md-6">
                <strong>Mileage:</strong>
                {{car.mileage}}
              </div>
              <div v-if="car.price>0" class="col-md-6" >
                <strong>Price:</strong>
                {{car.price | currency }}
              </div>
              <div v-else class="col-md-6" >
                <strong>Price:</strong>
                No Available
              </div>
              <div class="col-md-6">
                <a class="btn btn-success" target="blank" :href="car.url_to_site">Origin Website</a>
              </div>
            </div>
            <hr />
            <p class="card-text">
              <small class="text-muted">On Market from {{car.date_started_on_market}}</small>
            </p>
          </div>
        </div>
      </div>
      <Comment :carId="car.id"></Comment>
    </div>
    <EndFooter></EndFooter>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import NavBar from "@/components/NavBar.vue";
import Comment from "@/components/Comment.vue";
import Jumbotron from "@/components/Jumbotron.vue";
import EndFooter from "@/components/EndFooter.vue";

import axios from "axios";

export default {
  name: "detail",
  components: {
    NavBar,
    Jumbotron,
    EndFooter,
    Comment
  },
  data() {
    return {
      car: {}
    };
  },
  methods: {
    getCarDetails() {
      const Id = this.$route.params.carID;
      const path = "http://localhost:7070/api/v1.0/cars/";
      const fullpath = path + Id + "/";
      console.log(fullpath);
      axios
        .get(fullpath)
        .then(response => {
          console.log(response.data);
          this.car = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  created() {
    this.getCarDetails();
  }
};
</script>

