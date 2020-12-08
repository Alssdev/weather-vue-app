<template>
  <div class="box">
    <section class="columns mb-0">
      <div class="column">
        <p class="title is-3">{{ city.name }}</p>
      </div>
      <div class="column has-text-right">
        <p class="title is-3">{{ city.main.temp }} °C</p>
      </div>
    </section>
    <p>{{ city.weather[0].description }}</p>

    <div class="columns mt-1">
      <div class="column">
        <p><b>Max Temp:</b> {{ city.main.temp_max }} °C</p>
      </div>
      <div class="column">
        <p><b>Min Temp:</b> {{ city.main.temp_min }} °C</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    city: Object,
  },
};
</script>

<style></style>
