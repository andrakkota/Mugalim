<template>
  <div class="app">
    <Navigation />
    <router-view/>
  </div>
</template>

<script>
import Navigation from "./components/Navigation";
export default {
  name: "App",
  components: {
    Navigation,
  },
};
</script>

<style>




* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Roboto Light", sans-serif;
  font-weight: 400;
}

.app {
  min-height: 100vh;
  position: relative;
  background-color: #fcfcfc;
}


</style>
