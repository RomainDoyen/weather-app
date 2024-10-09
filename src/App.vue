<template>
  <div class="grid-container">
    <header class="header">
      <h1 class="animate__animated animate__slideInDown animate__delay-.5s"><i class="ri-sun-fill"></i> Weather App</h1>
    </header>
    <main class="main">
      <weather-view />
      <clock-view />
    </main>
    <footer class="footer">
      <p>@ 2022 Weather App</p>
    </footer>
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
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-height: 100vh;
  place-items: center;
}

.grid-container {
  display: grid;
  grid-template-areas: 
    "header"
    "main"
    "footer";
  grid-template-rows: auto 1fr auto;
  width: 100%;
  height: 100vh;
  background-color: #f3f3f3;
}

h1 {
  color: #3e4f60;
}

.ri-sun-fill {
  color: #d7c151;
}

.header {
  grid-area: header;
  text-align: center;
  padding: 20px;
}

.main {
  grid-area: main;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  padding: 20px;
  background-color: #B1D4E2;
}

.footer {
  grid-area: footer;
  text-align: center;
  padding: 20px;
  background-color: #3e4f60;
  color: #bbb;
}

@media (max-width: 768px) {
  .main {
    grid-template-columns: 1fr;
    padding: 10px;
  }

  .header, .footer {
    padding: 10px;
  }

  h1 {
    font-size: 1.5em;
  }
}

@media (max-width: 480px) {
  h1 {
    font-size: 1.2em;
  }

  .main {
    grid-template-columns: 1fr;
    gap: 10px;
    padding: 5px;
  }

  .footer {
    padding: 5px;
  }
}
</style>
