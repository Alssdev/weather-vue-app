<template>
  <div class="cityCard">
    <a class="delete" @click="remove"></a>
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
  </div>
</template>

<script>
export default {
  props: {
    city: Object,
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
