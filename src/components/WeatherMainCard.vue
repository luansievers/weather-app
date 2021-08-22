<template>
  <v-card-text>
    <v-row class="align-center justify-center">
      <v-col cols="2">
        <v-tooltip bottom v-if="currentWeather.weather[0]">
          <template v-slot:activator="{ on, attrs }">
            <v-img
                v-bind="attrs"
                v-on="on"
                class="float-right"
                :src="`http://openweathermap.org/img/wn/${currentWeather.weather[0].icon}@2x.png`"
                :alt="currentWeather.weather[0].description"
                width="92"
            ></v-img>
          </template>
          <span class="text-capitalize">{{ currentWeather.weather[0].description }}</span>
        </v-tooltip>
      </v-col>
      <div
          class="text-h2"
      >
        {{ currentWeather.main.temp }}&deg;C
      </div>
      <v-col
          cols="3"
      >
        Humidity: {{ currentWeather.main.humidity }}%<br>
        Wind: {{ currentWeather.wind.speed }} m/s
      </v-col>
    </v-row>
  </v-card-text>
</template>

<script>
export default {
  name: "WeatherMainCard",
  props: {
    currentWeather: {
      type: Object,
      required: true
    },
  },
}
</script>

<style scoped>

</style>