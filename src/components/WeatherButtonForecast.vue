<template>
  <v-card-actions>
    <v-row
        align="center"
        justify="space-around"
        class="mb-1"
    >
      <v-btn
          @click="getWeatherForecast"
          color="deep-purple lighten-2"
          text
      >
        SEE FORECAST
      </v-btn>
    </v-row>
  </v-card-actions>
</template>

<script>
export default {
  name: "WeatherButtonForecast",
  props: {
    cityId: {
      type: Number,
      required: true
    },
  },
  methods: {
    async getWeatherForecast() {
      try {
        const url = `http://api.openweathermap.org/data/2.5/forecast?id=${this.cityId}&appid=538882fc8387290c6cee83f313a6acf5&units=metric`
        let response = await fetch(url);
        let weatherForecast = await response.json();

        this.$emit('update:weatherForecast', weatherForecast.list)
        // this.$emit('update:availableDates', availableDates)
      } catch (error) {
        console.log(error);
      }
    },
  },
}
</script>

<style scoped>

</style>