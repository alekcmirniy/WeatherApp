<template>
  <div class="app-container">
    <h1>Local Weather Finder</h1>

    <div class="header-bar">
      <UpdateWidget />
      <p class="city-info">
        Check the weather for <strong>{{ city.trim() ? cityDisplay : "your location" }}</strong>
      </p>
    </div>

    <input
      v-model="city"
      type="text"
      placeholder="Type city name..."
      autocomplete="off"
    />
    <button
      :disabled="!city.trim()"
      @click="fetchWeather"
    >
      Get Weather
    </button>

    <p v-if="error" class="error-message">⚠️ {{ error }}</p>

    <section v-if="weatherData" class="weather-details">
      <p>🌡 Temperature: {{ weatherData.main.temp }} °C</p>
      <p>☁️ Condition: {{ weatherData.weather[0].main }}</p>
      <p>📝 Description: {{ weatherData.weather[0].description }}</p>
    </section>
  </div>
</template>

<script lang="ts">
import axios from 'axios';
import UpdateWidget from './components/UpdateWidget.vue';

interface WeatherData {
  main: { temp: number };
  weather: { main: string; description: string }[];
}

export default {
  components: { UpdateWidget },
  data() {
    return {
      city: '',
      error: '',
      weatherData: null as WeatherData | null,
    };
  },
  computed: {
    cityDisplay() {
      return this.city.trim();
    },
  },
  methods: {
    fetchWeather() {
      if (this.city.trim().length < 2) {
        this.error = 'Please enter at least 2 characters';
        this.weatherData = null;
        return;
      }
      this.error = '';
      this.weatherData = null;

      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${encodeURIComponent(
            this.city
          )}&units=metric&appid=f98d9b128bcb08311ddd8fb1eed8113a`
        )
        .then((res) => {
          this.weatherData = res.data;
        })
        .catch(() => {
          this.error = 'City not found or API error occurred';
        });
    },
  },
};
</script>

<style scoped lang="scss">
@use "sass:color";
$app-bg: #272727;
$primary-color: #76c7c0;
$button-bg: #45818e;
$button-hover: #659ea1;

.app-container {
  max-width: 700px;
  margin: 40px auto;
  padding: 25px 40px;
  background: $app-bg;
  border-radius: 25px;
  color: $primary-color;
  font-family: 'Verdana', sans-serif;
  box-shadow: 0 0 20px rgba(118, 199, 192, 0.6);
  text-align: center;
}

h1 {
  margin-bottom: 25px;
  font-weight: 700;
  letter-spacing: 1.3px;
}

.header-bar {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 30px;
  margin-bottom: 20px;

  .city-info {
    flex: 1;
    font-size: 1.1em;
    font-style: italic;
  }
}

input {
  padding: 10px 15px;
  font-size: 18px;
  border: none;
  border-radius: 12px;
  width: 60%;
  color: $app-bg;
  font-weight: 600;
  margin-right: 15px;
  outline: none;
}

input::placeholder {
  color: color.adjust($primary-color, $lightness: 30%);
}

button {
  background-color: $button-bg;
  color: #fff;
  border: none;
  padding: 12px 22px;
  border-radius: 12px;
  font-weight: 700;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;

  &:disabled {
    background-color: color.adjust($button-bg, $lightness: -15%);
    cursor: not-allowed;
  }

  &:not(:disabled):hover {
    background-color: $button-hover;
    transform: translateY(-4px);
  }
}

.error-message {
  margin-top: 18px;
  color: #ff6b6b;
  font-weight: 600;
}

.weather-details {
  margin-top: 30px;
  font-size: 1.2em;

  p {
    margin: 8px 0;
  }
}

</style>
