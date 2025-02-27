<template>
  <div class="app-container">
    <h1 class="title">Weather</h1>
    <CitySelector
      :cities="cities"
      v-model="selectedCity"
      @city-changed="fetchWeatherData"
    />
    <WeatherDisplay
      :data="data"
      :loading="loading"
      :error="error"
    />
  </div>
</template>

<script>
import CitySelector from "./components/CitySelector.vue";
import WeatherDisplay from "./components/WeatherDisplay.vue";

export default {
  components: {
    CitySelector,
    WeatherDisplay,
  },
  data() {
    return {
      loading: false,
      data: null,
      error: null,
      apiUrl: "https://api.openweathermap.org/data/2.5/forecast",
      apiKey: "0d5a268ee2d3ecbdeb3647f24af163b0",
      selectedCity: "Katowice",
      cities: ["Katowice", "Warsaw", "London", "Paris", "Berlin"],
    };
  },
  methods: {
    async fetchWeatherData() {
      try {
        this.loading = true;
        this.error = null;
        const response = await fetch(
          `${this.apiUrl}?q=${this.selectedCity}&units=metric&appid=${this.apiKey}`
        );

        if (!response.ok) {
          throw new Error(`Error with HTTP: ${response.status}`);
        }

        this.data = await response.json();
      } catch (err) {
        this.error = err.message || "Error with upload.";
      } finally {
        this.loading = false;
      }
    },
  },
  mounted() {
    this.fetchWeatherData();
  },
};
</script>

<style scoped>
.app-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
  background-color: #f7f7f7;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.title {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 20px;
  color: #333;
}
</style>
