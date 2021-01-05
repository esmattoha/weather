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
           <div class="location">{{weather.name}}</div>
           <div class="date">{{dateBuildup()}}</div>
         </div>
       </div>
       <div class="weather-box">
         <div class="temp"> degree C</div>
         <div class="weather">{{weather.weather}}</div>
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
      weather:{}
    }
  },
  methods:{
    fetchweather(e){
      if(e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&appid=${this.api_key}`)
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
