<template>
    <div class="centered-content">
      <div class="weather-widget">
        <div class="widget-header">
          <h2 class="widget-title">WEATHER </h2>
        </div>
        <q-input
          filled
          v-model="searchQuery"
          label="Masukkan Nama Kota"
          class="location-input"
        />
        <q-btn @click="searchWeather" class="search-button">Cari</q-btn>
        <div v-if="loading" class="loading-message">Loading data...</div>
        <div v-else-if="weatherData" class="weather-result">
          <div class="weather-info">
            <p class="city-name">{{ weatherData.name }}</p>
            <p class="temperature">{{ weatherData.main.temp }}°C</p>
            <img
              :src="getWeatherIconUrl(weatherData.weather[0].icon)"
              :alt="weatherData.weather[0].description"
              class="weather-icon"
            />
            <p class="weather-description">
              {{ weatherData.weather[0].description }}
            </p>
          </div>
          <div class="additional-info">
            <p>Kelembaban: {{ weatherData.main.humidity }}%</p>
            <p>Kecepatan Angin: {{ weatherData.wind.speed }} m/s</p>
          </div>
        </div>
        <div v-else-if="error" class="error-message">{{ error }}</div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from "vue";
  import axios from "axios";
  import { QInput, QBtn } from "quasar";
  
  export default {
    components: { QInput, QBtn },
    setup() {
      const searchQuery = ref("");
      const weatherData = ref(null);
      const loading = ref(false);
      const error = ref(null);
  
      const searchWeather = async () => {
        loading.value = true;
        error.value = null;
  
        try {
          const response = await axios.get(
            `https://api.openweathermap.org/data/2.5/weather?q=${searchQuery.value}&appid=bcbc6cc1860d02bd1f4306314c08d7e0&units=metric`
          );
          if (response.data.cod !== 200) {
            throw new Error("City not found");
          }
          weatherData.value = response.data;
        } catch (error) {
          console.error(error);
          error.value =
            "Gagal mengambil data cuaca atau kota tidak ditemukan";
        } finally {
          loading.value = false;
        }
      };
  
      const getWeatherIconUrl = (iconCode) => {
        return `https://openweathermap.org/img/wn/${iconCode}.png`;
      };
  
      return {
        searchQuery,
        weatherData,
        loading,
        error,
        searchWeather,
        getWeatherIconUrl,
      };
    },
  };
  </script>
  
  <style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

body {
  font-family: 'Poppins', sans-serif;
}

.centered-content {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: calc(100vh - 60px); /* Mengurangi tinggi navbar dari 100vh */
  margin-top: 90px; /* Jarak dari atas halaman */
}

.weather-widget {
  width: 400px; /* Ubah nilai width sesuai dengan kebutuhan */
  padding: 20px;
  border-radius: 15px; /* Meningkatkan radius */
  background-color: #f0f0f032;
  box-shadow: 0px 0px 20px 0px rgba(0, 0, 0, 0.2);
  background-position: center;
  text-align: center; /* Memastikan konten di tengah secara vertikal */
}

.widget-header {
  text-align: center;
  margin-bottom: 15px;
}

.widget-title {
  font-size: 1.8rem;
  color: #8B4513; /* Coklat */
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.location-input {
  width: calc(100% - 10px); /* Sesuaikan nilai width untuk menyesuaikan dengan tombol */
  padding: 12px;
  border: none;
  border-radius: 10px; /* Meningkatkan radius */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin: center;
  background-color: hwb(0 100% 0% / 0.34);
  color: #2F4F4F; /* Grey */
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.search-button {
  width: 110px; /* Ubah nilai width sesuai dengan kebutuhan */
  padding: 12px 25px;
  background-color: #B22222; /* Merah */
  color: #fff;
  border: none;
  border-radius: 10px; /* Meningkatkan radius */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 8px;
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.search-button:hover {
  background-color: #8B0000; /* Lebih gelap merah */
}

.loading-message {
  font-style: italic;
  color: #2F4F4F; /* Grey */
  margin-top: 10px;
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.weather-result {
  margin-top: 20px;
  padding: 15px;
  border-radius: 10px; /* Meningkatkan radius */
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s ease, transform 0.3s ease;
  background-color: hwb(0 100% 0% / 0.28);
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.weather-result:hover {
  box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.2);
  transform: translateY(-5px);
}

.weather-info {
  margin-bottom: 10px;
  text-align: center;
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.city-name {
  font-weight: bold;
  color: #8B4513; /* Coklat */
  font-size: 1.5rem;
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.temperature {
  font-size: 3rem;
  color: #0a0606; /* Merah */
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.weather-icon {
  width: 100px;
  height: 100px;
  margin: 0 auto;
  display: block;
}

.weather-description {
  font-style: italic;
  color: #4682B4; /* Biru */
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.additional-info {
  margin-top: 10px;
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.additional-info p {
  margin: 5px 0;
  color: #2F4F4F; /* Grey */
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}

.error-message {
  color: #B22222; /* Merah */
  margin-top: 10px;
  text-align: center;
  font-family: 'Poppins', sans-serif; /* Menggunakan Poppins */
}


  </style>
  