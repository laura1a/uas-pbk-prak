<template>
    <div class="widget-cuaca">
      <h2 class="judul-widget">Widget Cuaca</h2>
      <div class="input-lokasi">
        <label for="lokasi">Masukkan Lokasi:</label>
        <input type="text" id="lokasi" v-model="lokasi" />
        <button @click="ambilDataCuaca">Dapatkan Cuaca</button>
      </div>
      <div v-if="dataCuaca" class="data-cuaca">
        <p class="lokasi">Lokasi: {{ dataCuaca.name }}</p>
        <p v-if="dataCuaca.main" class="temperatur">
          Suhu: {{ dataCuaca.main.temp }}°C
        </p>
        <p v-if="dataCuaca.weather" class="deskripsi">
          Deskripsi: {{ dataCuaca.weather[0].description }}
        </p>
        <img
          v-if="dataCuaca.weather"
          :src="getWeatherImage(dataCuaca.weather[0].main)"
          :alt="dataCuaca.weather[0].description"
          class="cuaca-image"
        >
      </div>
      <p v-else-if="errorMessage" class="error-message">
        {{ errorMessage }}
      </p>
      <p v-else class="loading-message">Memuat data cuaca...</p>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        lokasi: '',
        dataCuaca: null,
        errorMessage: '',
        units: 'metric'
      };
    },
    methods: {
      async ambilDataCuaca() {
        try {
          const apiKey = 'b7bfca7b27a3485144fea086c50d09dc';
          const apiUrl = `https://api.openweathermap.org/data/2.5/weather?q=${this.lokasi}&units=${this.units}&appid=${apiKey}`;
          const response = await fetch(apiUrl);
          const data = await response.json();
          if (data.cod !== 200) {
            this.dataCuaca = null;
            this.errorMessage = data.message;
          } else {
            this.dataCuaca = data;
            this.errorMessage = '';
          }
        } catch (error) {
          this.dataCuaca = null;
          this.errorMessage = 'Failed to fetch weather data';
          console.error('Error mengambil data cuaca:', error);
        }
      }, 
      getWeatherImage(weather) {
      if (weather === 'Clear') {
        return 'https://cdn.pixabay.com/photo/2014/04/03/00/40/sun-309025_960_720.png'; 
      } else if (weather === 'Clouds') {
        return 'https://pic55.photophoto.cn/20200519/0020033057076033_b.jpg'; 
      } else if (weather === 'Rain') {
        return 'https://png.pngtree.com/png-clipart/20210224/ourlarge/pngtree-heavy-rain-raindrops-rainy-weather-png-image_2923914.jpg'; 
      } else if (weather === 'Drizzle') {
        return 'https://example.com/drizzle.png'; 
      } else if (weather === 'Mist') {
        return 'https://example.com/mist.png'; 
      } else if (weather === 'Fog') {
        return 'https://example.com/fog.png';
      } else if (weather === 'Haze') {
        return 'https://example.com/haze.png';
      } else {
        return 'https://example.com/unknown.png';
      }
    }
  }
};
</script>

<style scoped>
.widget-cuaca {
  font-family: Arial, sans-serif;
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 10px;
  background: linear-gradient(135deg, #cfd9df 0%, #e2ebf0 100%);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.judul-widget {
  text-align: center;
  color: #333;
  margin-bottom: 20px;
  font-size: 28px;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

.input-lokasi {
  display: flex;
  align-items: center;
  margin-top: 30px;
}

label {
  margin-right: 10px;
}

#lokasi {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 5px;
  padding: 10px 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  box-shadow: 0 3px 8px rgba(0, 0, 0, 0.1);
}

.button:hover {
  background-color: #0056b3;
}

.data-cuaca {
  margin-top: 40px;
  text-align: center;
}

.lokasi {
  font-weight: bold;
  font-size: 36px;
}

.temperatur {
  margin-top: 10px;
  font-size: 48px;
  font-weight: bold;
}

.deskripsi {
  margin-top: 10px;
  font-style: italic;
  font-size: 20px;
}

p {
  margin: 0;
}

.cuaca-image {
  display: block;
  max-width: 200px;
  margin: 20px auto;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  animation: fadeIn 1s;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>