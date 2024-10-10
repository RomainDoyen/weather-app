<template>
    <div class="content-weather">
        <div class="enter-city animate__animated animate__pulse animate__repeat-2 animate__delay-1s">
            <SearchForm v-model="data.city" @submit="getWeather" />
        </div>
        <div class="weather animate__animated animate__backInLeft animate__delay-.5s" v-if="data.weather">
            <p>{{ data.weather.name }}, {{ data.weather.sys.country }}</p>
            <h1>{{ Math.round(data.weather.main.temp) }}&deg;C</h1>
            <p>{{ data.weather.weather[0].description }}</p>
            <p>Humidité : {{ data.weather.main.humidity }}%</p>
        </div>
        <!-- <div v-else v-pre>
            <p>Erreur, veuillez entrer une ville correcte</p>
        </div> -->
        <div class="w animate__animated animate__backInLeft animate__delay-.5s" v-if="data.weather">
            <p><i class="ri-windy-fill"></i> {{ data.weather.wind.speed }} km/h</p>
            <p><i class="ri-cloud-windy-fill"></i> {{ data.weather.wind.gust }} km/h</p>
        </div>
        <div v-else>
            <!-- <p>Erreur, veuillez entrer une ville correcte</p> -->
        </div>
    </div>
</template>

<script>
import { reactive } from 'vue'
import axios from 'axios'
import SearchForm from '../ui/SearchForm.vue'

export default {
    components: {
        SearchForm
    },
    name: 'WeatherView',
    setup() {
        let data = reactive({
            city: '',
            weather: null
        })

        const apiUrl = 'https://api.openweathermap.org/data/2.5/weather'
        const api_key = process.env.VUE_APP_API_KEY

        const getWeather = () => {
        axios(`${apiUrl}?units=metric&q=${data.city}&lang=fr&appid=${api_key}`)
        .then(res => {
            data.weather = res.data
            if(data.weather.weather[0].main.indexOf('Rain') > 0) {
                document.body.className = 'rainy';
            } else if(data.weather.weather[0].main.indexOf('Cloud') > 0) {
                document.body.className = 'cloudy';
            } else if(data.weather.weather[0].main.indexOf('Sunny') > 0) {
                document.body.className = 'sunny';
            }
        }).catch(err => console.log(err));
        }

        return {
            data,
            getWeather
        }
    }
}
</script>

<style>
.content-weather {
  font-family: "Montserrat", sans-serif;
  font-weight: 500;
  font-size: 1.3em;
  color: rgb(63, 102, 186);
  display: grid;
  align-items: center;
  justify-content: space-evenly;
  flex-wrap: wrap;
  align-content: center;
}

p {
    margin-top: 10px;
    margin-bottom: 15px;
}

i {
    font-size: 32px;
    vertical-align: middle;
}

.w {
    display: inline;
    flex-direction: column;
    align-items: center;
}

.weather {
    transition: all .1s ease-out;
    transition-timing-function: ease-in-out;
}

.w, .weather {
    background-color: #fff;
    border-radius: 5px;
    padding: 20px;
    margin: 20px;
}

.weather:focus-visible {
    transition-property: opacity, left;
    transition-duration: .3s, .5s;
}

h1 {
  margin: 0 auto;
  text-align: center;
  font-size: 4em;
  margin-bottom: 25px;
  z-index: 1000;
  position: relative;
}

@media (max-width: 900px) { 
    .content-weather {
        align-items: center;
        flex-direction: column;
        height: auto;
    }
    .enter-city input {
        margin-top: 20px;
        width: auto;
    }
    h1 {
        font-size: 3rem;
    }
    .list-group {
        margin-top: 20px;
    }
}
</style>