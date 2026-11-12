<template>
  <div id="app">
    <main>
      <div class="searchbox">
        <input
          type="text"
          class="search-bar"
          placeholder="Search for a city..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">UK</div>
          <div class="date">October 10, 2023</div>
        </div>
      </div>
      <div class="weather-box">
        <div class="temp">20°C</div>
        <div class="weather">Rain</div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "ba3ef9e77c0147a9b99132825262610",
      url_base:
        "https://api.weatherapi.com/v1/current.json?key=ba3ef9e77c0147a9b99132825262610&q=London",
      query: "",
      weather: {},
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "monsterrat", sans-serif;
}
main {
  min-height: 100vh;
  padding: 25px;
}
.search-bar {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: none;
  font-size: 16px;
  background-color: #f0f0f0;
}
</style>
