<template>
  <div id="app">
  <Weather />
  </div>
</template>

<script>
import Weather from "./components/Weather.vue";

export default {
  name: "App",
  components: {
    Weather
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #FFF ;
  background: {
    position:center;
    repeat:no-repeat;
    image:  url('../src/assets/manila-1709394_1920.jpg');
    size: cover;
  }
  height: 100%;
  position: fixed;
  width: 100%;
  margin:0;
}
* {
  margin: 0;
}

</style>
