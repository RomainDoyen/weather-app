<template>
    <div class="content-weather">
        <div class="enter-city animate__animated animate__pulse animate__repeat-2 animate__delay-1s">
            <input v-model="data.city" @keyup.enter="getWeather" placeholder="Entrer vôtre ville" type="text">
            <i class="ri-send-plane-2-fill"></i>
        </div>
        <div class="weather animate__animated animate__backInLeft animate__delay-.5s"  v-if="data.weather">
            <p>{{ data.weather.name }}, {{ data.weather.sys.country }}</p>
            <h1>{{ Math.round(data.weather.main.temp) }}&deg;C</h1>
            <p>{{ data.weather.weather[0].description }}</p>
            <p>Humidité : {{ data.weather.main.humidity }}%</p>
        </div>
        <div class="w animate__animated animate__backInLeft animate__delay-.5s" v-if="data.weather">
            <p><i class="ri-windy-fill"></i> {{ data.weather.wind.speed }} km/h</p>
            <p><i class="ri-cloud-windy-fill"></i> {{ data.weather.wind.gust }} km/h</p>
        </div>
    </div>
</template>

<script>
import { reactive } from 'vue'
import axios from 'axios'

export default {
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
        }).catch(err => console.log(err))
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
  height: 50vh;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
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

.ri-send-plane-2-fill {
    margin-left: 10px;
    background-color: rgb(63, 102, 186);
    color: white;
    border-radius: 5px;
    padding: 7px;
}

.weather {
    transition: all .1s ease-out;
    transition-timing-function: ease-in-out;
}

.weather:focus-visible {
    transition-property: opacity, left;
    transition-duration: .3s, .5s;
}

.enter-city input {
    border: none;
    outline: none;
    border-radius: 5px;
    padding: 15px;
    width: 50vh;
    font-size: 20px;
    color: #ec0062;
    font-weight: 400;
    box-shadow: 2px 2px 10px 0px rgba(119, 119, 119, 0.59);
    -moz-box-shadow: 2px 2px 10px 0px rgba(119, 119, 119, 0.59);
    -webkit-box-shadow: 2px 2px 10px 0px rgba(119, 119, 119, 0.59);
}

h1 {
  margin: 0 auto;
  text-align: center;
  font-size: 4em;
  margin-bottom: 25px;
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