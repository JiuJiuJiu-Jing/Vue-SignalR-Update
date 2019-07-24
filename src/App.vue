<template>
  <div id="app">
    
    <router-view/>
  </div>
</template>

<script>

const signalR= require('@aspnet/signalr')

// import * as signalR from "@aspnet/signalr"

export default {
  name: 'App',
  created:function() {

    //   let thisVue = this;



    // thisVue.connection = new signalR.HubConnectionBuilder()
    // .withUrl('http://localhost:50170/api/chatHub')
    // .configureLogging(signalR.LogLevel.Information)
    // .build();

    // thisVue.connection.on("sayHi",function(msg){
    //     console.log(msg);
    // });

    // thisVue.connection.start().then(()=>{
    //   this.connection.invoke("hello").catch(function(err){
    //     return console.error(err);
    //   });
    // });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
