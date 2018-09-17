<template>
  <div id="app">
    <h1 class="uk-heading-divider">Kitsu</h1>
    <card-list></card-list>
  </div>
</template>

<script>
import CardList from "./components/CardList.vue";
//import UIkit from "uikit";

export default {
  name: "app",
  components: {
    CardList
  }
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  width: 90%;
  margin-left: auto;
  margin-right: auto;
}
</style>
