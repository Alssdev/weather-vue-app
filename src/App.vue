<template>
  <div>
    <navBar></navBar>

    <div class="section">
      <section>
        <div class="field is-grouped">
          <div class="control is-expanded">
            <input
              v-model="city"
              type="text"
              name="city"
              id="city"
              placeholder="Search your city"
              class="input is-dark"
            />
          </div>
          <div class="control">
            <button class="button is-dark">
              Search
            </button>
          </div>
        </div>
      </section>

      <!-- city cards -->
      <section class="mt-5">
        <div class="columns is-multiline">
          <div class="column is-4">
            <city-card></city-card>
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

export default {
  name: 'App',

  components: {
    navBar: NavBar,
    'city-card': CityCard,
  },

  data: () => ({
    city: '',
  }),

  methods: {},
};
</script>

<style></style>
