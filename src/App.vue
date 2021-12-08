<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.weather[0].main=='Rain' ? 'rain' : ''">
    <main>
      <div class="search-box">
          <input 
                type="text" 
                class="search-bar" 
                v-model="search" 
                placeholder="Search..."
                @keyup.enter="getData">
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="weather-content">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <p class="date">8 Desember 2021</p>
          <div class="date"></div>
          <div class="weather-temp">
            <div class="temp">{{  Math.round(weather.main.temp) }} C</div>
          </div>

          <div class="weather-name">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>  
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      api_key: '28020839d6e2827fe42140823694c1e5',
      base_url: 'https://api.openweathermap.org/data/2.5/',
      search: '',
      weather: {}
    }
  },
  
  methods: {
    getData(){

      fetch(this.base_url + `weather?q=${this.search}` + `&units=metric&APPID=${this.api_key}`)
      .then(response => response.json())
      .then(this.setResult)
    },

    setResult(result){
      this.weather = result;
    }
  }
}
</script>

<style>
  * {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
  }

  body {
    font-family: Arial, Helvetica, sans-serif
  }

  main {
    min-height: 100vh;
    padding: 25px;
    /* background: red; */
    background-image: linear-gradient(to bottom, rgba(255,255,255,0.10), rgba(255,255,255,0.25));
  }

  #app {
    background-image: url('./assets/bg3.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  #app.rain {
    background-image: url('./assets/bg2.jpg');
  }


  .search-box {
    /* background: red; */
    width: 100%;
    padding: 30px;
  }

  .search-box .search-bar {
    display: block;
    width: 100%;
    font-size: 28px;

    appearance: none;
    outline: none;
    background: none;
    border: none;

    padding: 15px;

    background-color: rgba(255,255,255,0.5);
    border-radius: 0px 16px 0px 16px;
    transition: 0.4s;
  }

  .search-box .search-bar:focus {
    background-color: rgba(255,255,255,0.75);
    border-radius: 16px 0px 16px 0px;
  }

  .weather-wrap {
    width: 600px;
    margin: auto;
    /* border: 1px solid black; */
    text-align: center;
  }

  .weather-content .location {
    font-size: 72px;
    font-weight:900;
    font-style: italic;
    color: rgb(255, 255, 255);
  }

  .date {
    font-size: 38px;
    font-style: italic;
    color: rgb(255, 255, 255);
    margin-bottom: 20px;
  }

  .weather-temp {
    width: 350px;
    height: 150px;
    margin: auto;
    border: 1px solid rgb(248, 228, 228);
    background-color: rgba(255,255,255,0.5);
    border-radius: 10px;
    margin-bottom: 20px;
  }

  .temp {
    font-size: 130px;
    font-weight: 1000;
    color: rgb(255, 255, 255);
    font-style: italic;
  }

  .weather-name {
    font-size: 72px;
    font-weight: 900;
    font-style: italic;
    color: rgb(255, 255, 255);
  }
  
</style>
