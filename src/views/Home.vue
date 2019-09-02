<template>
  <div>
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <NavBar></NavBar>
    <Jumbotron title="Web Car Scraper" pathTo="cars" titleButton="Search Cars"></Jumbotron>
    <div class="container">
      <h1 class="mb-4">Last Cars Scraped</h1>
      <div class="row">
        <div v-for="car in carList" :key="car.id" class="col-xs-12 col-sm-6 col-lg-3 mb-4">
          <CardCar :car="car"></CardCar>
        </div>
      </div>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import NavBar from "@/components/NavBar.vue";
import Jumbotron from "@/components/Jumbotron.vue";
import CardCar from "@/components/Car/CardCar.vue";
import Footer from "@/components/Footer.vue";

import axios from "axios";

export default {
  name: "home",
  components: {
    NavBar,
    Jumbotron,
    CardCar,
    Footer
  },
  data() {
    return {
      carList: []
    };
  },
  methods: {
    getCarList() {
      const path = "http://localhost:7070/api/v1.0/cars/";
      axios
        .get(path, {
          params: {
            ordering: '-date_scraped'
          }
        })
        .then(response => {
          this.carList = response.data.results;
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  created() {
    this.getCarList();
  }
};
</script>
