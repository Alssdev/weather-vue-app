<template>
  <div>
    <navBar></navBar>

    <div class="section">
      <h2 class="title has-text-centered">Know the climate of your city</h2>
      <section>
        <div class="field is-grouped">
          <div class="control is-expanded">
            <input
              v-model="cityName"
              type="text"
              name="city"
              id="city"
              placeholder="Search your city..."
              class="input is-dark"
            />
          </div>
          <div class="control">
            <button @click="fetchWeatherData" class="button is-dark">
              Search
            </button>
          </div>
        </div>
      </section>

      <!-- city cards -->
      <section class="mt-5">
        <div class="columns is-multiline">
          <div v-for="city in cities" :key="city.sys.id" class="column is-4">
            <city-card :city="city" @remove="removeCity(city)"></city-card>
          </div>
        </div>
      </section>
    </div>
    <!-- search bar -->
  </div>
</template>

<script>
import NavBar from '@/components/Navbar';
import CityCard from '@/components/CityCard';
import axios from 'axios';

import { apiKey } from './api';

export default {
  name: 'App',

  components: {
    navBar: NavBar,
    'city-card': CityCard,
  },

  data: () => ({
    cityName: '',
    cities: [],
  }),

  methods: {
    async fetchWeatherData() {
      if (this.cityName) {
        try {
          const response = await axios.get(
            `http://api.openweathermap.org/data/2.5/weather?q=${this.cityName}&appid=${apiKey}`
          );
          const city = response.data;

          // Kelvin degrees to Celsius
          let temp = city.main.temp;
          temp = parseFloat(temp - 273.15).toFixed(2);
          city.main.temp = temp;

          let temp_min = city.main.temp_min;
          temp_min = parseFloat(temp_min - 273.15).toFixed(2);
          city.main.temp_min = temp_min;

          let temp_max = city.main.temp_max;
          temp_max = parseFloat(temp_max - 273.15).toFixed(2);
          city.main.temp_max = temp_max;

          this.cities.push(city);
          this.cityName = null;
        } catch (error) {
          console.log(error.code);
        }
      }
    },

    removeCity(city) {
      this.cities.splice(this.cities.indexOf(city), 1);
    },
  },
};
</script>

<style></style>
