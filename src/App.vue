<template>
  <div id="app">
    <insuranceApp />
  </div>
</template>

<script>
import insuranceApp from "./components/insuranceApp.vue";

export default {
  name: "App",
  components: {
    insuranceApp,
  },
};
</script>

<style>
body {
  background: linear-gradient(90deg, #2b303a 0%, #3f4756 100%);
  margin: 0;
}
#app {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
