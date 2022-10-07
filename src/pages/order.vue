<template>
  <div>
    <order-header></order-header>
    <router-view></router-view>
    <!-- <service-bar></service-bar> -->
    <nav-footer></nav-footer>
  </div>
</template>

<script>
import OrderHeader from "./../components/OrderHeader.vue"
import ServiceBar from "./../components/ServiceBar.vue";
import NavFooter from "./../components/NavFooter.vue";

export default {
  name: "order",
  data(){
    return{
      title:"",
      tip:""
    }
  },
  components: {
    OrderHeader,
    ServiceBar,
    NavFooter,
  },
};
</script>