<template>
  <div id="app">
    <div class="intro">
      <h1>Castel-Clima</h1>
      <p>Bienvenido a Castel-Clima, esta pequeña App te mostrara el clima del hoy gracias a la API de <b>OpenWeather</b> y <b>WeatherStack</b>, solo escribe de forma correcta la ciudad de donde quieres conocer el clima y listo.</p>
    </div>
    <clima/>
    <footer>Esteban Javier Castelblanco García</footer>
  </div>
</template>

<script>
  import clima from "./components/clima.vue";
  export default {
    name: 'App',
    components: {
      clima
    }
  }
</script>

<style>
  body{
    width: 100vw;
    background-color: #333;
    color: #fff;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
  }

  .intro{
    width: 80%;
    margin: 60px auto;
  }

</style>
