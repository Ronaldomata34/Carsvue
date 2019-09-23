<template>
  <div>
    <NavBar></NavBar>
    <Jumbotron title="Web Car Scraper" pathTo="home" titleButton="Go to Home"></Jumbotron>
    <div class="container mt-4">
      <hr />
      <div class="row">
        <div class="col-md-12 col-lg-3 col-sm-12 mb-4 filter-section" style="height:100%">
          <CarFilter @filterData="updateCarsData"></CarFilter>
        </div>
        <div class="col-md-12 col-lg-9 col-sm-12">
          <ListCar :data="carsData.results"></ListCar>
          <Pagination v-if="!carsData.results == []" @nextData="updateCarsData" :info="carsData"></Pagination>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from "@/components/NavBar.vue";
import Jumbotron from "@/components/Jumbotron.vue";
import Pagination from "@/components/Pagination.vue";
import CarFilter from "@/components/Car/CarFilter.vue";
import ListCar from "@/components/Car/ListCar.vue";

export default {
  name: "cars",
  components: {
    Jumbotron,
    NavBar,
    CarFilter,
    ListCar,
    Pagination
  },
  data() {
    return {
      carsData: ""
    };
  },
  methods: {
    updateCarsData(variable) {
      this.carsData = variable;
    }
  }
};
</script>

<style lang="css" scoped>
.filter-section {
  height: 100%;
  padding-top: 0;
  color: white;
}
</style>