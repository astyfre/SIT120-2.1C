<template>
  <img alt="Vue logo" src="./assets/Anabolic-Lifestyle-logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <br>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: linear-gradient(to bottom right, lightblue, darkblue);
  padding: 60px;
  
}
img{
  display: block;
  margin-left: auto;
  margin-right: auto;
  max-width: 15%;
  height:auto;
  min-width: 10%;
  padding: 10px 10px;
}
</style>
