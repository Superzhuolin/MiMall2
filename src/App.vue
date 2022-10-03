<template>
  <div id="app">
  </div>
</template>

<script>
import axios from "axios";
import jsonp from "jsonp";
export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      age: 30,
      data: "",
    };
  },
  // mounted(){
  //   let url ='http://github.com/easy-mock/easy-mock'
  //    axios.get(url).then(()=>{
  //    });
  // },
  mounted() {
    let url = "https://www.imooc.com/activity/servicetime";
    // axios(url).then(() => {});
     
  },
};
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