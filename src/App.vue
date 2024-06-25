<template>
  <div id="app">
    <Navbar />
    <router-view />
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";

export default {
  components: {
    Navbar,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  font-family: Arial;
}
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
#page-wrap {
  margin: auto;
  max-width: 800px;
  width: 100%;
  min-height: 100vh;
  padding: 16px;
}

button {
  background-color: #41b883;
  border: none;
  border-radius: 8px;
  color: white;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
  outline: 0;
  padding: 16px;
  width: 100%;
  box-sizing: border-box;
}

</style>
