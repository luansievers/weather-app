<template>
  <v-row class="align-center justify-center mt-2 mb-1">
    <v-chip-group>
      <v-chip v-for="(value,key) in availableDates" :key="key" @click="goToDate(key)">
        {{ key }} - {{ new Date(key) | moment("dddd (MMMM)") }}
      </v-chip>
    </v-chip-group>
  </v-row>
</template>

<script>
export default {
  name: "WeatherForecastDatesChips",
  props: {
    weatherForecast: {
      type: Array,
      required: true
    },
  },
  computed: {
    availableDates() {
      let dates = Array.from(this.weatherForecast, item => this.$moment(item.dt_txt).format('L'))
      let availableDates = {}
      dates.forEach(function (item) {
        availableDates[item] = (availableDates[item] || 0) + 1
      });
      return availableDates;
    }
  },
  methods: {
    goToDate(date) {
      this.$emit('update:page', Math.ceil(this.weatherForecast.findIndex(item => this.$moment(item.dt_txt).format('L') === date) / 4))
    },
  },
}
</script>

<style scoped>

</style>