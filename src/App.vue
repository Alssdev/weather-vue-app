<template>
  <div>
    <navBar></navBar>

    <!-- search bar -->
    <section class="section">
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
  </div>
</template>

<script>
import navBar from '@/components/Navbar';

export default {
  name: 'App',

  components: {
    navBar,
  },

  data: () => ({
    city: '',
  }),

  methods: {},
};
</script>

<style></style>
