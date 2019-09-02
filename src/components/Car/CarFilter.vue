<template>
  <form>
    <div class="row row-1">
      <div>
        <div class="col-md-12">
          <h3>Search By Brand and Model</h3>
        </div>
        <div class="col-md-6 col-lg-12 col-sm-6">
          <div class="input-group mb-3">
            <div class="input-group-prepend">
              <label class="input-group-text" for="inputGroupSelect01">Brand</label>
            </div>
            <select
              name="make"
              @change="getModels()"
              v-model="makeSelected"
              class="custom-select"
              id="inputGroupSelect01"
            >
              <option value>Choose brand</option>
              <option v-for="make in makes" :value="make.key" :key="make.id">{{make.name}}</option>
            </select>
          </div>
        </div>
      </div>
      <div class="col-md-6 col-lg-12 col-sm-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <label class="input-group-text" for="inputGroupSelect01">Model</label>
          </div>
          <select
            name="model"
            v-model="modelSelected"
            class="custom-select"
            id="inputGroupSelect01"
          >
            <option value>Choose model</option>
            <option
              v-for="model in models"
              :value="model.id"
              :key="model.id"
            >{{model.name}}</option>
          </select>
        </div>
      </div>
      <div class="col-md-6 col-lg-12 col-sm-6">
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <label class="input-group-text" for="inputGroupSelect01">Zipcode</label>
          </div>
          <input
            v-model="zipcodeSelected"
            required="true"
            name="zipcode"
            type="type"
            class="form-control"
            placeholder
            aria-label="Example text with button"
            aria-describedby="button-addon1"
          />
        </div>
      </div>
      <div class="col-md-6 col-lg-12 col-sm-6">
        <div class="form-group">
          <label for="formControlRange">Min Mileage: {{minMileage}} miles</label>
          <input
            @change="onChangeRange()"
            min="80000"
            step="10000"
            max="300000"
            v-model="minMileage"
            type="range"
            class="form-control-range"
            id="formControlRange"
          />
        </div>
      </div>
      <div class="col-md-6 col-lg-12 col-sm-6">
        <div class="form-group">
          <label for="formControlRange">Max Mileage: {{maxMileage}} miles</label>
          <input
            :min="minMileage"
            step="10000"
            max="300000"
            v-model="maxMileage"
            type="range"
            class="form-control-range"
            id="formControlRange"
          />
        </div>
      </div>
      <div class="col-md-6 col-lg-12 col-sm-6">
        <button @click.prevent="getFilter()" class="btn btn-success">Search</button>
      </div>
    </div>
  </form>
</template>

<script>
import axios from "axios";

export default {
  name: "CarFilter",
  data() {
    return {
      cars: [],
      makes: new Array(),
      models: new Array(),
      makeSelected: "",
      modelSelected: "",
      zipcodeSelected: "",
      minMileage: 80000,
      maxMileage: 300000
    };
  },
  methods: {
    getMakes() {
      const path = "http://localhost:7070/api/v1.0/makes/";
      axios
        .get(path)
        .then(response => {
          this.makes = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    },
    getModels() {
      const path = "http://localhost:7070/api/v1.0/makes/";
      axios
        .get(path, {
          params: {
            key: this.makeSelected
          }
        })
        .then(response => {
          console.log(response.data);
          this.models = response.data[0].models;
        })
        .catch(error => {
          console.log(error);
        });
    },
    getFilter() {
      const path = "http://localhost:7070/api/v1.0/cars/";
      axios
        .get(path, {
          params: {
            model: this.modelSelected,
            zip_code: this.zipcodeSelected,
            min_mileage: this.minMileage,
            max_mileage: this.maxMileage,
          }
        })
        .then(response => {
            console.log(response.data);
            this.$emit("filterData", response.data);
          //this.models = response.data[0].models;
        })
        .catch(error => {
          console.log(error);
        });
      //this.$store.commit("addListCarSection", carInfo.data);
    }
  },
  created() {
    this.getMakes();
  }
};
</script>

<style lang="css" scoped>
.row-1 {
  padding: 20px;
  color: white;
}

form {
  background-color: #062142;
  -webkit-box-shadow: -5px 6px 13px -2px rgba(0, 0, 0, 0.64);
  -moz-box-shadow: -5px 6px 13px -2px rgba(0, 0, 0, 0.64);
  box-shadow: -5px 6px 13px -2px rgba(0, 0, 0, 0.64);
}
</style>