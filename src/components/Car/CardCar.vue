<template>
  <div class="card mb-4">
    <img v-if="car.main_picture" :src="car.main_picture" class="card-img" alt />
    <img
      v-else
      src="https://static1.cargurus.com/gfx/cg/noImageAvailable_large.png"
      class="card-img"
      alt
    />
    <div class="card-body d-flex justify-content-between">
      <div class="info-1">
        <p>
          <strong>Model:</strong>
          {{car.model.name}}
        </p>
        <p>
          <strong>Make:</strong>
          {{car.model.make}}
        </p>
      </div>
      <div class="info-2">
        <p>
          <strong>Year:</strong>
          {{car.year}}
        </p>
        <p>
          <strong>Price:</strong>
          ${{car.price}}
        </p>
      </div>
    </div>
    <button class="btn btn-success">View More</button>
    <a class="btn btn-dark" :href="car.url_to_site" role="button">Origin Website</a>
  </div>
</template>

<script>
export default {
  name: "CardCar",
  props: {
    car: Object
  }
};
</script>

<style lang="css" scoped>
div.card {
  -webkit-box-shadow: 10px 10px 5px -8px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 10px 10px 5px -8px rgba(0, 0, 0, 0.75);
  box-shadow: 10px 10px 5px -8px rgba(0, 0, 0, 0.75);
  border-radius: 0;
}

p {
  margin: 0;
}

.info-1 {
  margin-bottom: 4px;
}

.btn {
  border: 0;
  border-radius: 0;
  color: white;
  font-weight: 800;
}

</style>