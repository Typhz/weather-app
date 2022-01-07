<template>
  <main id="app">
    <!-- <video autoplay muted loop id="myVideo">
      <source src="../../assets/background-video.mp4" type="video/mp4" />
    </video> -->
    <h1 id="title">A única previsão que você precisa</h1>
    <hr />
    <div id="search-container">
      <SearchInput @city="submit" />
      <Loading v-if="isLoading"/>
      <div id="weather-info" v-if="weatherData">
        <div>
          <h1>
            {{ weatherData.main.temp }}
            <sup>ºC</sup>
          </h1>
        </div>
        <div>
          <h4>{{ weatherData.name }} - {{ weatherData.sys.country }}</h4>
          <h6>{{ weatherData.weather[0].description }}</h6>
        </div>
      </div>
    </div>
   
  </main>
</template>

<script>
import axios from "axios";
import SearchInput from "../../components/AppSearchInput";
import Loading from "../../components/AppLoading";
let apiKey = process.env.VUE_APP_API_KEY
export default {
  name: "App",
  components: {
    SearchInput,
    Loading,
  },
  data() {
    return {
      userName: "",
      weatherData: "",
      isLoading: false, 
    };
  },
  methods: {
    submit(city) {
      this.isLoading = true
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric&lang=pt_br`
        )
        .then((response) => (this.weatherData = response.data))
        .finally(() => (this.isLoading = false));
    },
  },
};
</script>

<style>
@import "../../styles/globalStyles.css";
#myVideo {
  position: fixed;
  right: 0;
  bottom: 0;
  z-index: -1;
  min-width: 100%;
  min-height: 100%;
}

h1{
  font-weight: 400;
}
h1#title{
  text-align: center;
  padding: 0 1rem;
}
#app {
  height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  display: flex;
}

#weather-info {
  background-color: rgba(71, 71, 71, 0.479);
  backdrop-filter: blur(20px);
  width: 30vw;
  min-height: 5vh;
  padding: 1rem 2rem;
  margin-top: 2%;
  border-radius: 0.5rem;
  flex-wrap: wrap;
  justify-content: space-between;
  display: flex;
}

#search-container {
  align-items: center;
  flex-direction: column;
  display: flex;
}

hr {
  background-color: rgba(167, 167, 167, 0.356);
  width: 10%;
  height: 2%;
  margin: 1.4rem 0;
  border-radius: 0.5rem;
  border: none;
}
@media only screen and (max-width: 600px) {
  #weather-info {
    width: 70vw;
  }
}
</style>
