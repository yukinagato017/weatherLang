<template>
  <div class="hello" >
    <div class="nav">
      <form v-on:submit.prevent="getWeather(query)">
        <input type="text" placeholder="Search City" v-model="query" @keyup="getWeather(query)"> 
        <button class="btn" v-on:click="getLocation()" v-if="query <= 0">Get weather by location</button>
     </form>
    </div>

    <div class="home"  v-if="typeof results.main != 'undefined'">
      <div class="title-wrap">
        <h1>{{ results.name }} , {{results.sys.country}}</h1>
      </div>
      <div class="temp-wrap">
        <h1>{{Math.round(results.main.temp - 273.15)}}&#8451;</h1>
        <span class="main">{{results.weather[0].main}}</span> <br>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "Weather",
  data () {
    return {
      api_key: '209aee5aca64a2a38eceee62745bc1cb',
      auth_key:'f4d582642c22103599f512ceb1d548a3',
      url_base:'https://ipinfo.io/json',
      query: '',
      results:{},
      ip:'178.128.209.84',
      name: '',
      weatherType: ""
    }
  },
  methods: {
    getWeather(query) {
      axios.get('https://api.openweathermap.org/data/2.5/weather?q=' + query + '&appid=' + this.api_key).then(response => {
        this.results = response.data;
          this.weatherType = response.data.weather[0].main;

      })
    },
     getLocation() {
     axios.get('http://api.ipstack.com/' + this.ip + '?access_key=' + this.auth_key + '&format=1').then(response => {
        this.query = response.data.city;
     });
   }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
$searchColor: #FFFF;
$backgroundCenter: center;
@mixin borderStyle{
  border-left-style:none;
  border-right-style:none;
  border-top-style: none;
}
.hello {
  margin: 0px 8px;
  padding: 0px 14px;
}
.nav {
  padding: 20px 0px;
  width:100%;
  overflow:hidden;
  margin: 0px 5px;
  a {
    font-weight: bold;
    color: #FFF;
    text-align: left;
    text-decoration: none;
    margin-left: 40px;
  }
}
input[type=text] {
  @include borderStyle;
  float: right;
  padding: 10px 15px;
  width: 300px;
  background-color: transparent;
  outline-style: none;
  position: relative;
  top: -10px;
  color:$searchColor;
  font-size:20px;
  margin: 0px -12px;
}
.home {
  text-align: $backgroundCenter;

  .title-wrap {
    font-size: 4vw;
    position: relative;

  }
  .temp-wrap {
    font-size: 70px;

  }
}
.date {
  color: $searchColor;

  font-size: 20px;
  text-align: $backgroundCenter;
}
.main {
  color: $searchColor;
  font-size: 60px;
  text-align: $backgroundCenter;
}
.btn {
    outline: none;
    outline-style: none;
    border: none;
    border-radius: 16vw;
    padding: 1vw 1xvw;
    font-size: 16px;
    cursor: pointer;
    position:left;
}
::placeholder { 
  color: $searchColor;
}

:-ms-input-placeholder {
  color: $searchColor;
}

::-ms-input-placeholder { 
  color: $searchColor;
}
</style>
