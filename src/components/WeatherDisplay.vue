<template>
    <div class="weather-display">
      <div v-if="loading" class="loading">Loading...</div>
  
      <div v-if="error" class="error">
        Error: {{ error }}
      </div>
  
      <ul v-if="data && !loading" class="weather-list">
        <li
          v-for="(item, index) in data.list.slice(0, 10)"
          :key="index"
          class="weather-item"
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
  </template>
  
  <script>
  export default {
    props: {
      data: Object,
      loading: Boolean,
      error: String,
    },
  };
  </script>
  
  <style scoped>
  .weather-display {
    margin-top: 20px;
  }
  
  .loading {
    text-align: center;
    font-size: 1.2rem;
    color: #555;
  }
  
  .error {
    text-align: center;
    color: red;
    font-size: 1.2rem;
  }
  
  .weather-list {
    list-style: none;
    padding: 0;
    margin: 0;
  }
  
  .weather-item {
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 5px;
    padding: 15px;
    margin-bottom: 10px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }
  </style>
  