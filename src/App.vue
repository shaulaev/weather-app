<script>
import Weather from './components/Weather.vue'

export default {
  name: "App",
  data() {
    return {
      city: "",
      weather: "",
      pending: false
    }
  },
  components: {
    Weather: Weather
  },
  methods: {
    getWeatherByCity() {
      if(this.city.trim().length < 2) {
        alert("Too short")
      } else {
        this.pending = true
        fetch(`https://api.weatherapi.com/v1/current.json?key=8ccdc3d653f341709f5150317230403&q=${this.city}&aqi=no&lang=ru`).then(d => d.json()).then(data => this.weather = data).then(() => this.pending = false)
      }
    }
  },

  computed: {
    setCity() {
      return "«" + this.city + "»"
    },
  }
}
</script>

<template>
  <div class="content">
    <h1 class="title">Weather App <img class="cloud" src="//cdn.weatherapi.com/weather/64x64/day/122.png" alt=""></h1>

    <p>Проверь погоду в городе {{ city === "" ? "своем!" : setCity }}</p>

    <div class="form">
      <input v-model="city" type="text" placeholder="Write your city">
      <button class="check" @click="getWeatherByCity()">Check</button>
    </div>

    <Weather v-if="weather.current && !this.pending" :weather="weather"/>

    <div class="lds-ripple" v-else-if="this.pending"><div></div><div></div></div>

  </div>
</template>

<style scoped>
  .content {
    max-width: 500px;
    min-height: fit-content;
    border-radius: 50px;
    padding: 20px 90px 70px 90px;
    background-color: #1f1f1f;
    color: #ffffff;
    display: flex;
    flex-direction: column;
    align-items: center;
    position: relative;
  }

  .content .title {
    user-select: none;
  }

  .content input {
    width: 200px;
    height: 40px;
    border-radius: 5px;
    padding: 5px;
    border: none;
    outline: none;
    transition: .2s;
    margin-right: 5px;
  }

  .content .check {
    height: 40px;
    display: flex;
    align-items: center;
  }

  .content input:focus {
    transition: .2s;
    border: 1px solid rgb(0, 153, 255);
  }

  .cloud {
    position: absolute;
    top: 40px;
    right: 20px;
  }

  .lds-ripple {
    margin-top: 30px;
    display: inline-block;
    position: relative;
    width: 80px;
    height: 80px;
  }
  .lds-ripple div {
    position: absolute;
    border: 4px solid #fff;
    opacity: 1;
    border-radius: 50%;
    animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
  }
  .lds-ripple div:nth-child(2) {
    animation-delay: -0.5s;
  }

  @keyframes lds-ripple {
    0% {
      top: 36px;
      left: 36px;
      width: 0;
      height: 0;
      opacity: 0;
    }
    4.9% {
      top: 36px;
      left: 36px;
      width: 0;
      height: 0;
      opacity: 0;
    }
    5% {
      top: 36px;
      left: 36px;
      width: 0;
      height: 0;
      opacity: 1;
    }
    100% {
      top: 0px;
      left: 0px;
      width: 72px;
      height: 72px;
      opacity: 0;
    }
  }

  .content .form {
    display: flex;
    flex-wrap: wrap;
  }

  @media screen and (max-width: 630px) {

    .content .form input, .content .form button {
      margin-right: 0;
      width: 100%;
    }

    .content .form button {
      margin-top: 10px;
    }

    .content .title {
      font-size: 40px;
      display: flex;
    }
    .content .cloud {
      top: 8px;
      right: 21px;
    }

    .content {
      padding: 20px;
    }
  }

 @media screen and (max-width: 320px) {
  
  .content .title {
    font-size: 30px;
  }

  .content .cloud {
    top: -2px;
  }

 }

</style>
