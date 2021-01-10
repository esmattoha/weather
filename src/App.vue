<template>
  <div id="#app">
    <main class="main">
      <div class="search-box">
        <input type="text" class="search" 
        placeholder="Search..." 
        v-model="query"
        @keypress="fetchweather"
        />
      </div>
     
       <div class="weather-wrap">
         <div class="location-box">
          <!-- Checking if weather object is null. if null then do not print data  -->
           <div class="location" v-if="weather">{{weather.name}}</div>
           <div class="date">{{dateBuildup()}}</div>
         </div>
       </div>
        <!-- Checking if weather object is null. if null then do not print data  -->
       <div class="weather-box" v-if="weather">
        <!-- weather object has main key inside main key there is another key called temp which is the temperature -->
         <div class="temp"> {{weather.main.temp}} ° C</div>
         <!-- Weather has an array wether it's not an object so in order to access an array you have to access it through index not key**  -->
         <div class="weather">{{weather.weather[0].main}} <br>
           <small>{{weather.weather[0].description}}</small>
         </div>
       </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data(){
    return{
      api_key:'c97283cde2c0a43b427c06b329197c72',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:null
    }
  },
  methods:{
    fetchweather(e){
      if(e.key == "Enter"){
        //metric query parameter shows temp in celius
        fetch(`${this.url_base}weather?q=${this.query}&appid=${this.api_key}&units=metric`)
        .then(res=>{
          return res.json();
        }).then(this.setResults);
        
      }
    },
    setResults(result){
      this.weather =result ;
    },
    dateBuildup(){
      let d = new Date();
      let months = ['January', 'February','March', 'April','May','June','July', 'August' , 
      'September', 'October','November' , 'December'];
      let days = ['Sunday','Monday','Tuesday','Wednesday','Thrusday','Friday', 'Sutarday'];

      let day = days[d.getDay()];
      let date = d.getDate() ;
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  font-family: sans-serif;
}
#app{
  background-image: url('./assets/cold.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
.main{
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25 ), rgba(0, 0, 0, 0.75));
}
.search-box {
  margin: 0 auto;
  padding: 15px;
  text-align: center;
  
}
.search-box .search {
  font-family: sans-serif;
  font-size: 25px;
  border-radius: 0 16px 0 16px;
  background-color: rgb(191, 197, 185);
  padding: 3px 5px;
  outline: none;
  border: none;
  box-shadow: 0 3px rgba(0, 0, 0, 0.25 );
}
.location-box .location{
  color: rgb(255, 255, 255);
  font-size: 40px;
  font-weight: 500;
  text-align: center;
  text-shadow: 0 3px rgba(0, 0, 0, 0.25 );
  font-family: cursive;
}
.location-box .date{
  color: rgb(255, 255, 255);
  font-size: 28px;
  font-weight: 200;
  text-align: center;
  text-shadow: 0 3px rgba(0, 0, 0, 0.25 );
  font-family: cursive;
  font-style: italic;
}

.weather-box{
  text-align: center;
}
.weather-box .temp{
  display: inline-block;
  color: #fff;
  padding: 15px 25px;
  font-size: 30px;
  text-shadow: 0 2px rgba(0, 0, 0, 0.5);
  background-color: rgba(125, 125, 125, 1.25 );
  border-radius: 10px;
  margin: 30px 0;
  box-shadow: 4px 6px rgba(0, 0, 0, 0.25 );

}
.weather-box .weather{
  font-size: 40px;
  font-weight: 300;
  color: #fff;
  font-style: italic;
  text-shadow: 0 4px rgba(0, 0, 0, 0.25 );
}

</style>
