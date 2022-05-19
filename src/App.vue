<template>
  <div class="content">
    <h1 class="animate__animated animate__slideInDown animate__delay-.5s"><i class="ri-sun-fill"></i> Weather App</h1>
    <div class="content-app">
      <weather-view />
      <clock-view />
      <div class="footer">
        <p>@ 2022 Weather App</p>
      </div>
    </div>
  </div>
</template>

<script>
import WeatherView from './components/WeatherView.vue'
import ClockView from './components/ClockView.vue'
import 'remixicon/fonts/remixicon.css'

export default {
  name: 'App',
  components: {
    WeatherView,
    ClockView
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,900');
@import url('https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css');

*, ::before, ::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  min-height: 100vh;
  display: grid;
	grid-template-rows: auto 1fr auto;
}

.ri-sun-fill {
  color: #d7c151;
  font-size: 60px;
}

.content-app {
  background-image: linear-gradient(
    to right top,
    #99bbcb,
    #a5c7d7,
    #b1d4e2,
    #bde0ee,
    #c9edfa
  );
}

.footer {
  background-color: #3e4f60;
  width: 100%;
  padding: 50px;
}

.footer p {
  color: #bbb;
}

#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #3e4f60;
  margin-top: 20px;
}
</style>
