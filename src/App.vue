<template>
  <div id="app">
    <Scale />
  </div>
</template>

<script>
import Scale from "./components/Scale.vue";

export default {
  name: "App",
  components: {
    Scale,
  },
};
</script>

<style>
#app {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

:root {
  --text-color: #303030;
}

html,
body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  font-family: freight-text-pro;
  background: #f3f0ec;
}

@media only screen and (max-width: 760px) {
  #app {
    justify-content: start;
  }
}
</style>
