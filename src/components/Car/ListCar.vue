<template>
  <div>
    <div v-for="car in data" :key="car.id" class="card p-4 mb-4">
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
                {{car.model.make}}
              </div>
              <div class="col-md-6">
                <i class="fa fa-comment"></i> <span> {{car.comments}}</span>
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
              <div v-if="car.price>0" class="col-md-6">
                <strong>Price:</strong>
                {{car.price | currency}}
              </div>
              <div v-else class="col-md-6">
                <strong>Price:</strong>
                No Available
              </div>
              <div class="col-md-6">
                <a class="btn btn-success" target="blank" :href="car.url_to_site">Origin Website</a>
              </div>
              <div class="col-md-6">
                <router-link
                  class="btn btn-info"
                  :to="{ name: 'detail', params: { carID: car.id }}"
                >View More</router-link>
              </div>
            </div>
            <hr />
            <p class="card-text">
              <small class="text-muted">On Market from {{car.date_started_on_market}}</small>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListCar",
  props: ["data"]
};
</script>

<style lang="css" scoped>
</style>