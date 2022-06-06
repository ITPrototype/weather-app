<script>
import axios from 'axios';
export default {
  data(){
    return{
      api_key:'25d37c82f4eb30addb056eba55638870',
      cityname:'London',
      wind:'',
      feels_like:'',
      temp:'',
      humidity:'',
      pressure:'',
      description:'',
      icon:''
    }
  },
  methods:{
    async getWeather(){
      try{
        const response = 
              await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.cityname}&appid=${this.api_key}&units=metric`)
        console.log(response.data);
        this.temp = response.data.main.temp;
        this.wind = response.data.wind.speed;
        this.humidity = response.data.main.humidity;
        this.pressure = response.data.main.pressure;
        this.feels_like = response.data.main.feels_like;
        this.description = response.data.weather[0].description;
        this.icon = response.data.weather[0].icon;
      }
      catch(err){
        console.log(err);
      }  
    }
  },
  mounted(){
    this.getWeather()
  }
}
</script>

<template>
  <div class="wrapper">
    <div class="ellipse1"></div>
    <div class="ellipse2"></div>
    <div class="ellipse3"></div>
    <div class="container">
      <h3 class="name">{{cityname}}</h3>
      <h1 class="temprature">{{temp}}°C</h1>
      <div class="img">
        <img :src="`http://openweathermap.org/img/wn/${icon}@2x.png`" class="icon" alt="icon"/>
      </div>
      <h6 class="description">{{description}}</h6>
      <div class="about">
        <div class="wind-block"><i class="fa-solid fa-wind"></i> <h5 class="wind">Wind: {{wind}} km/h</h5></div>
        <div class="pressure-block"><i class="fa-solid fa-compress"></i> <h5 class="wind">Pressure: {{pressure}} p</h5></div>
        <div class="humidity-block"><i class="fa-solid fa-droplet"></i> <h5 class="wind">Humidity: {{humidity}} %</h5></div>
        <div class="feels-block"><i class="fa-solid fa-fire"></i> <h5 class="wind">Feels like: {{feels_like}} ~</h5></div>
      </div>
      
    </div>
  </div>
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@200&display=swap');
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Sarabun', sans-serif;
  }
  body{
    background-color: black;
  }
  .wrapper{
    width: 100%;
    height: 500px;
    .ellipse1{
      width: 800px;
      height: 800px;
      position: absolute;
      top: -370px;
      left: -202px;
      background: linear-gradient(131.03deg, #26D0CE 7.78%, #1A2980 89.77%);
      filter: blur(5px);
      border-radius: 50%;
    }
    .ellipse2{
      position: absolute;
      width: 450px;
      height: 450px;
      left: 1025px;
      top: 300px;
      background: linear-gradient(90deg, #FF4E50 0%, #F9D423 100%);
      filter: blur(2px);
      backdrop-filter: blur(2px);
      border-radius: 50%;
    }
    .ellipse3{
      position: absolute;
      width: 75px;
      height: 75px;
      left: 937px;
      top: 75px;
      border-radius: 50%;
      background: linear-gradient(90deg, #EC008C 0%, #FC6767 100%);
      backdrop-filter: blur(5px);
      filter: blur(1px);
    }
  }
  .container{
    width: 448px;
    height: 560px;
    margin: 100px auto;
    background: linear-gradient(143.98deg, rgba(255, 255, 255, 0.11) 0%, rgba(255, 255, 255, 0.22) 100%);
    backdrop-filter: blur(50px);
    border-radius: 30px;
    padding: 10px;
    .name{
      color:white;
      text-align: center;
      padding-top: 30px;
      letter-spacing: 4px;
    }
    .temprature{
      color: #fff;
      text-align: center;
      font-weight: 700;
      font-size: 50px;
      margin-top: 20px;
      letter-spacing: 2px;
    }
    .description{
      color: gray;
      text-align: center;
      font-size: 20px;
      letter-spacing: 2px;
      margin-top: 10px;

    }
  }
  .about{
    display: flex;
    flex-wrap: wrap;
    color: white;
    justify-content: space-between;
    width: 350px;
    margin: 40px auto;
    .wind-block{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      width: 170px;
      padding: 20px;
      letter-spacing: 1px;
    }
    .pressure-block{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      width: 180px;
      padding: 20px;
      letter-spacing: 1px
    }
    .humidity-block{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      width: 160px;
      padding: 20px;
      letter-spacing: 1px
    }
    .feels-block{
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      width: 180px;
      padding: 20px;
      letter-spacing: 1px
    }
  }
  .img{
    margin: 10px auto;
    width: 100px;
  }
  .search{
    margin: 10px auto;
    width: 200px;
    .search-input{
      border: none;
      outline: none;
      background: none;
      color:white;
      font-size: 20px;
      font-weight: 500;
      border-bottom: 2px solid gray;
    }
  }
</style>

