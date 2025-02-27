<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">Weather</h1>

    
    <div class="mb-4">
      <label for="city-select" class="block font-medium mb-2">Select city:</label>
      <select
        id="city-select"
        v-model="selectedCity"
        @change="fetchWeatherData"
        class="p-2 border rounded"
      >
        <option v-for="city in cities" :key="city" :value="city">{{ city }}</option>
      </select>
    </div>

    
    <div v-if="loading" class="text-center">
      <p>Loading data...</p>
    </div>

    
    <div v-if="data && !loading" class="weather-list">
      <ul class="flex flex-col gap-4">
        <li
          v-for="(item, index) in data.list.slice(0, 10)"
          :key="index"
          class="weather-item border p-4 rounded-md shadow-md"
        >
          <p><strong>Date and time:</strong> {{ item.dt_txt }}</p>
          <p>
            <strong>Temperature:</strong>
            {{ Math.round(item.main.temp) }}°C
          </p>
          <p><strong>Weather:</strong> {{ item.weather[0].description }}</p>
        </li>
      </ul>
    </div>

    
    <div v-if="error" class="text-red-500 text-center">
      <p>Error: {{ error }}</p>
    </div>
  </div>
</template>

<script>
export default {
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
          throw new Error(`Error HTTP: ${response.status}`);
        }

        this.data = await response.json();
        console.log(this.data);
      } catch (err) {
        this.error = err.message || "Error with getting date.";
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
.container {
  max-width: 600px;
}

.weather-item {
  background-color: #f9f9f9;
}
</style>
