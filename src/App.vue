<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <button v-on:click="loadData">Load Data</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios';
export default {
  name: 'App',
  components: {
    HelloWorld
  },
    methods: {
    loadData: function() {
        console.log('Try and get Lambda Response')
        axios.get('https://upq4sdk6d2.execute-api.us-east-2.amazonaws.com/default/vue-test').then(response => {
        //this.$http.get('https://upq4sdk6d2.execute-api.us-east-2.amazonaws.com/default/vue-test').then(response => {
        console.log(response);
      }, response => {
        console.log(response);
      });
    }
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
}
</style>
