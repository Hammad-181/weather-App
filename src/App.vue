<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 20 ? 'warm' : '' ">
    <main>
      <div class="container">
        <div class="section">
          Search with a city name
        </div>

         <div class="search-box">
        <input type="text"  
        class="search-bar"
        placeholder="Search..."
        v-model="query"
        @keypress="fetchWeather"
        />
      </div>
          <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
            <div class="location-box">
              <div class="location">{{weather.name}},{{weather.sys.country}}</div>
              <div class="date">Saturday, 19th March 2022</div>
            </div>

           <div class="weather-box">
            <div class="temp">{{Math.trunc(weather.main.temp)}}°C</div>
            <div class="weather">{{weather.weather[0].main}}</div>
           </div>
          </div>
    
      </div>
         </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      apiKey: "470ffcc3d31d23ca23544ca5bade0b77",
      urlBase: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather : {},
      error: '',
    }
    
  },
  methods:{
    fetchWeather(e){
      if(e.key === "Enter"){
        fetch(`${this.urlBase}weather?q=${this.query}&units=metric&APPID=${this.apiKey}`)
        .then(res => res.json()).then(this.setResults)
      }
    },
    setResults(results){
      this.weather = results;
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: "montserrat", sans-serif;
}

#app{
  background-size: cover;
  background-position:bottom;
  background-image: url("./assets/brown-and-gray-dock-wallpaper-preview.jpeg");
  transition: 0.4s;

}

#app.warm{
  background-image: url("./assets/uplifting-rays-of-sunshine-wallpaper-preview.jpeg")
}
main{
  min-height:100vh;
  padding:25px;
}
.search-box{
  width:100%;
  margin-bottom: 30px;
}
.search-box .search-bar{
  display:block;
  width: 100%;
  padding: 15px;
  color: #313131;

  font-size: 20px;

  outline: none;
  appearance: none;
  border: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius : 0px 16px 0px 16px;

}

.location-box .location {
  color: #fff;
  font-size: 30px;
  font-weight:500;
  text-align: center;
  text-shadow:1px 3px rgba(0, 0 ,0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight:300;
  font-style: oblique;
  text-align: center;
  text-shadow:1px 3px rgba(0, 0 ,0, 0.25);
}
.weather-box{
  text-align: center;
}

.weather-box .temp {
  display:inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 120px;
  font-weight:900;

  text-shadow: 3px 6px rgba(0, 0 ,0, 0.25);
  background-color:rgba(255, 255 ,255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow:3px 6px rgba(0, 0 ,0, 0.25)
  
}
.weather-box .weather {
  color: #fff;
  font-size: 50px;
  font-weight:700;
  font-style:oblique;

  text-shadow: 3px 6px rgba(0, 0 ,0, 0.25);
  
}
.section{
  padding: 15px;
  margin-bottom: 10px;
  font-size: 50px;
  text-align:center;
  font-style: italic;
  color:aliceblue;
  text-shadow: 3px 6px rgba(0, 0 ,0, 0.3);
}
</style>
