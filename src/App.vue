<template>
  <v-app id="inspire">
    <weather-app-bar></weather-app-bar>

    <v-main class="grey lighten-3">
      <v-container>
        <v-row class="justify-center">
          <v-col
              cols="6"
          >
            <v-card elevation="0" rounded="lg">
              <weather-city-selector :currentWeather.sync="currentWeather"
                                     @clear="clearData">
              </weather-city-selector>
              <template v-if="currentWeather && !weatherForecast">
                <weather-main-card :current-weather="currentWeather">
                </weather-main-card>
                <weather-button-forecast :city-id="currentWeather.id"
                                         :weatherForecast.sync="weatherForecast">
                </weather-button-forecast>
              </template>
            </v-card>
          </v-col>

          <v-col
              cols="12"
              sm="10"
              v-if="weatherForecast"
          >
            <v-card elevation="0" rounded="lg">
              <weather-forecast-card :weather-forecast="weatherForecast">
              </weather-forecast-card>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>

import WeatherAppBar from "@/components/WeatherAppBar";
import WeatherCitySelector from "@/components/WeatherCitySelector";
import WeatherMainCard from "@/components/WeatherMainCard";
import WeatherButtonForecast from "@/components/WeatherButtonForecast";
import WeatherForecastCard from "@/components/WeatherForecastCard";

export default {
  name: 'App',

  components: {WeatherForecastCard, WeatherButtonForecast, WeatherMainCard, WeatherCitySelector, WeatherAppBar},

  data() {
    return {
      currentWeather: null,
      weatherForecast: null
    }
  },
  methods: {
    clearData() {
      this.currentWeather = null
      this.weatherForecast = null
    },
  }
}
</script>
