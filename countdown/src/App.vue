<script>
import { RouterLink, RouterView } from 'vue-router'
import Countdown from './components/Countdown.vue'
export default {
  name: "App",
  components: {
    Countdown,
  },
  data(){
    return {
      end: new Date("2023-01-14T12:00:00"),
    };
  },
  methods: {
    finish(){
      console.log('Finish');
    },
  },
};
</script>

<template>
  <div id="app">
   
    <Countdown :date="end" @onFinish="finish()"></Countdown>
  </div>
</template>
<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  width: 100%;
  position: relative;
  text-align: center;
  
}
</style>