<template>
  <v-card-text>
    <v-row class="justify-center">
      <v-col cols="8">
        <v-autocomplete
            v-model="city"
            :items="cities"
            :item-text="(item)=> `${item.name}, ${item.country}`"
            item-value="id"
            label="City"
            clearable
            hint="Please select city to see forecast"
            :persistent-hint="!city"
            @change="getCurrentWeather"
            @click:clear="clearData"
            :loading="loading"
        >
        </v-autocomplete>
      </v-col>
    </v-row>
  </v-card-text>
</template>

<script>
export default {
  name: "WeatherCitySelector",
  data() {
    return {
      loading: false,
      city: null,
      cities: [
        {
          "id": 6167865,
          "name": "Toronto",
          "country": "CA"
        },
        {
          "id": 6094817,
          "name": "Ottawa",
          "country": "CA"
        },
        {
          "id": 1850147,
          "name": "Tokyo",
          "country": "JP"
        }
      ],
    }
  },
  methods: {
    clearData() {
      this.$emit('clear')
    },
    async getCurrentWeather() {
      if (!this.city){
        return
      }
      this.loading = true
      try {
        const url = `http://api.openweathermap.org/data/2.5/weather?id=${this.city}&appid=538882fc8387290c6cee83f313a6acf5&units=metric`
        let response = await fetch(url);
        let currentWeather = await response.json();
        this.$emit('update:currentWeather', currentWeather)
      } catch (error) {
        console.log(error);
      }
      this.loading = false
    },
  },
}
</script>

<style scoped>

</style>