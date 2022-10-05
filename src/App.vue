<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import axios from "axios";
import jsonp from "jsonp";
export default {
  name: "App",
  components: {
  },
  data() {
    return {
      age: 30,
      data: "",
    };
  },
  mounted() {
     
  },
};
</script>

<style>
</style>