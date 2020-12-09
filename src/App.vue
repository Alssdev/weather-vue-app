<template>
  <div>
    <navBar></navBar>

    <div class="section">
      <h2 class="title has-text-centered">Know the climate of your city</h2>
      <!-- search bar -->
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
              :class="{ 'is-loading': isFetchingData }"
            />
          </div>
          <div class="control">
            <button
              class="button is-dark"
              :class="{ 'is-loading': isFetchingData }"
              @click="fetchWeatherData"
            >
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

    <div class="modal" :class="{ 'is-active': isModalActive }">
      <div class="modal-background" @click="isModalActive = false"></div>
      <div class="modal-content">
        <article class="message is-danger">
          <div class="message-header">
            <p>City not found</p>
          </div>
          <div class="message-body">
            It seems that your city could not be found. Please review that you
            have written the name of the city correctly
          </div>
        </article>
      </div>
      <button
        class="modal-close is-large"
        aria-label="close"
        @click="isModalActive = false"
      ></button>
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/Navbar';
import CityCard from '@/components/CityCard';
import axios from 'axios';

import { apiKey, endPoint } from './api';

export default {
  name: 'App',

  components: {
    navBar: NavBar,
    'city-card': CityCard,
  },

  data: () => ({
    cityName: '',
    cities: [],

    // interface
    isFetchingData: false,
    isModalActive: false,
  }),

  methods: {
    async fetchWeatherData() {
      if (this.cityName) {
        this.isFetchingData = true;

        const params = {
          q: this.cityName,
          appid: apiKey,
        };

        try {
          const response = await axios.get(endPoint, { params });

          this.cities.push(response.data);
          this.cityName = null;
        } catch (error) {
          // show error message
          this.isModalActive = true;
        }

        this.isFetchingData = false;
      }
    },

    removeCity(city) {
      this.cities.splice(this.cities.indexOf(city), 1);
    },

    closeModal() {},
  },
};
</script>

<style></style>
