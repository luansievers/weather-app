<template>
  <v-container fluid>
    <v-data-iterator :items="weatherForecast" hide-default-footer :items-per-page="4" :page="page">
      <template v-slot:default="props">
        <v-row>
          <v-col
              v-for="item in props.items"
              :key="item.name"
              cols="12"
              sm="6"
              md="4"
              lg="3"
          >
            <v-card>
              <v-card-title>
                {{ new Date(item.dt_txt) | moment("dddd (MMMM | HH a)") }}
              </v-card-title>
              <v-card-text>
                <v-row class="align-center justify-center">
                  <v-col cols="3">
                    <v-tooltip bottom v-if="item.weather[0]">
                      <template v-slot:activator="{ on, attrs }">
                        <v-img
                            v-bind="attrs"
                            v-on="on"
                            class="float-right"
                            :src="`http://openweathermap.org/img/wn/${item.weather[0].icon}@2x.png`"
                            :alt="item.weather[0].description"
                            width="92"
                        ></v-img>
                      </template>
                      <span class="text-capitalize">{{ item.weather[0].description }}</span>
                    </v-tooltip>
                  </v-col>
                  <div
                      class="text-h4"
                  >
                    {{ item.main.temp }}&deg;C
                  </div>
                  <v-col
                      cols="4"
                      class="caption"
                  >
                    Humidity: {{ item.main.humidity }}%<br>
                    Wind: {{ item.wind.speed }} m/s
                  </v-col>
                </v-row>
                <v-row class="align-center justify-center">
                  <div
                      class="caption"
                  >
                    Min: {{ item.main.temp_min }}&deg;C - Max: {{ item.main.temp_max }}&deg;C
                  </div>
                </v-row>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
        <v-btn
            v-if="page > 1"
            color="pink"
            fab
            dark
            small
            absolute
            top
            left
            @click="formerPage"
        >
          <v-icon>mdi-chevron-left</v-icon>
        </v-btn>
        <v-btn
            v-if="page < numberOfPages"
            color="pink"
            fab
            dark
            small
            absolute
            top
            right
            @click="nextPage"
        >
          <v-icon>mdi-chevron-right</v-icon>
        </v-btn>
      </template>
    </v-data-iterator>
    <weather-forecast-dates-chips :weather-forecast="weatherForecast" :page.sync="page">
    </weather-forecast-dates-chips>
  </v-container>
</template>

<script>
import WeatherForecastDatesChips from "@/components/WeatherForecastDatesChips";
export default {
  name: "WeatherForecastCard",
  components: {WeatherForecastDatesChips},
  props: {
    weatherForecast: {
      type: Array,
      required: true
    },
  },
  data() {
    return {
      page: 1,
    }
  },
  computed: {
    numberOfPages() {
      return Math.ceil(this.weatherForecast.length / 4)
    },
  },
  methods: {
    nextPage() {
      if (this.page + 1 <= this.numberOfPages) this.page += 1
    },
    formerPage() {
      if (this.page - 1 >= 1) this.page -= 1
    },
  },
}
</script>

<style scoped>

</style>