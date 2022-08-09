<template>

<div id="app">
  <main class="main">
 <div class="box-opcao">
   <div class="info-box"><fa class="info" icon="info"></fa><p>
Consuming weather API</p></div>    
     <input 
     v-model="query" 
    @keypress="fetchWeather" 
    type="text" 
    placeholder="Search here... Ex: São Paulo">    
 </div>
<div v-if="typeof weather.main != 'undefined'" >
  <div class="box-local" v-if="typeof weather.main != 'undefined'"  >
    <div>{{weather.name}},{{weather.sys.country}}</div>
  </div>
  <div class="box-tempo" >
    <fa 
    class="icon cloud"
    icon="cloud"
    :class="typeof weather.main != 'undefined' && weather.weather[0].main == 'Clouds' ? 'active' : ''"
     />
    <fa 
    class="icon sun"
     icon="sun"
     :class="typeof weather.main != 'undefined' && weather.weather[0].main == 'Clear' ? 'active' : ''"
     />
    <fa 
    class="icon bolt"
    icon="bolt"
    :class="typeof weather.main != 'undefined' && weather.weather[0].main == 'Rain' ? 'active' : ''"
    />
    <div class="clima">{{weather.weather[0].main}}</div>
    <div class="temp"
     :class="typeof weather.main != 'undefined' && weather.main.temp > 15 ? 'active' : ''"
    >{{Math.round(weather.main.temp)}} ° C</div>
  </div>
  </div>
  <status></status>  
  </main>
</div>

</template>

<script>

import Status from './components/Status';

export default {
    
    name: 'App',
    components: {
    Status
},

data() {

  return{

    query: '',
    weather: {},
  }  
},
methods: {

    
 
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`https://api.openweathermap.org/data/2.5/weather?q=${this.query}&units=metric&APPID=89e1fb5304ab099dd13fcf679f42ecd2`)      
          .then(res => {
             return res.json();
          }).then(this.setResults);
      }
    },setResults (results) {
      this.weather = results;
      
    } 

  }
      
}




</script>

<style>

@import './assets/css/app.css';

#app{
 
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;

}

.main{

  height: 90vh;
  border-radius: 15px;
  width: 70%;
  background: var(--grey);
  display: flex;
  flex-direction: column;
  box-shadow: 0px 5px 8px var(--grey-0-0);
  justify-content: space-evenly;
 
}
.info-box{
  display: flex;
  height: 50px;
  align-items: center;
  justify-content: center;
  
}
.info{
  font-size: 10px ;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  background: var(--grey);
  margin: 10px; 
}
.sun{
 display: none;
}
.sun.active{
  display:inline;
}
.cloud{
  display: none;
}
.cloud.active{
  display:inline;
}
.bolt{
  display: none;
}
.bolt.active{
  display: inline;
}

.box-opcao{
  
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  animation: init  3s ;
}
@keyframes init{
  0%{
    transform: translatey(-50px);
    opacity: 0.2;
  }
}
.box-local{

  color: var(--white-1);
  height: 90px;
  font-size: 23px;
  font-weight: 700;
 
}
.icon{
 
  font-size: 120px;
  color: var(--white);
}

.box-tempo{
 
  color: var(--white-1);
  font-weight: 700;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.clima{

  font-size: 23px;
}
.temp{
  font-size: 25px;
  color: var(--blue-0);
}
.temp.active{
  color: var(--cor-principal);
}
 input {

        height: 60px;
        width: 400px;
        outline: none;
        border: none;
        border: 2px solid var(--grey-1);  
        color: var(--cor-principal); 
        border-radius: 7px;
        text-align: center;
        padding: 7px;
        font-size: 25px;
                            
    }
    input::placeholder{

          color: var(--grey-0-0);
         
    }
    input:hover::-webkit-input-placeholder{

    color: var(--cor-principal);
    transition: all 0.4s ease-in;
    }
    input:focus,
    input:focus::-webkit-input-placeholder{
        color: var(--cor-principal);
        transition: all 0.4s ease-in;
        border-color: var(--cor-principal);
    }
  @media (max-width: 600px) {

      .main{
         width: 100%;
      }
      input{
        width: 90%;
        
      }

      input::placeholder{
      font-size: 20px;
      }
  }
</style>
