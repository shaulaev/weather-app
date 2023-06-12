<script>
    export default {
        name: "Weather",
        props: {
            weather: Object
        },
        created() {
            console.log(this.weather)
        },
        computed: {
            setCityName() {
            return "Название Города: " + this.weather.location.name
            },
            setTempInCelsium() {
            return "Температура в цельсиях: " + this.weather.current.temp_c + "°C"
            },
            setTempFeelsLikeCelsium() {
            return "По ошущению: " + this.weather.current.feelslike_c + "°C"
            },
            setCondition() {
            return "На данный момент " + this.weather.current.condition.text.toLowerCase()
            }
        }
    }
</script>

<template>
    <div class="weather">
      <img :src="weather.current.condition.icon" alt="">
      <p>{{ setCityName }}</p>
      <p>{{ setTempInCelsium }}</p>
      <p>{{ setTempFeelsLikeCelsium }}</p>
      <p>{{ setCondition }}</p>
    </div>
</template>

<style>
  .weather {
    width: 100%;
    margin: 10px;
    padding: 10px;
    border-radius: 40px;
    background-color: #101010;
  }
</style>