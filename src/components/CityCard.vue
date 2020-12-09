<template>
  <div class="cityCard">
    <a class="delete" @click="remove"></a>
    <div class="box">
      <section class="columns mb-0">
        <div class="column">
          <p class="title is-3">
            {{ cityName }}
            <span class="title is-5 has-text-primary">
              {{ country }}
            </span>
          </p>
        </div>
        <div class="column has-text-right">
          <p class="title is-3">{{ temp }} °C</p>
        </div>
      </section>
      <p>{{ description }}</p>

      <div class="columns mt-1">
        <div class="column">
          <p><b>Max Temp:</b> {{ tempMax }} °C</p>
        </div>
        <div class="column">
          <p><b>Min Temp:</b> {{ tempMin }} °C</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    city: Object,
  },

  computed: {
    cityName() {
      return this.city.name;
    },
    country() {
      return this.city.sys.country;
    },
    description() {
      return this.city.weather[0].description;
    },
    temp() {
      // Kelvin degrees to Celsius
      let temp = this.city.main.temp;
      temp = parseFloat(temp - 273.15).toFixed(2);

      return temp;
    },
    tempMax() {
      let tempMax = this.city.main.temp_min;
      tempMax = parseFloat(tempMax - 273.15).toFixed(2);

      return tempMax;
    },
    tempMin() {
      let tempMin = this.city.main.temp_max;
      tempMin = parseFloat(tempMin - 273.15).toFixed(2);

      return tempMin;
    },
  },

  methods: {
    remove() {
      this.$emit('remove');
    },
  },
};
</script>

<style scoped>
.cityCard:hover .delete {
  opacity: 1;
}

.delete {
  opacity: 0;
  transition: 0.1s;
}
</style>
