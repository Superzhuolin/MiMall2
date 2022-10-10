<template>
  <div class="index"></div>
</template>
<script>
import ServiceBar from "./../components/ServiceBar.vue";
import Modal from "./../components/Modal.vue";
import { swiper, swiperSlide } from "vue-awesome-swiper";
import "swiper/dist/css/swiper.css";

export default {
  name: "index",
  components: {
    ServiceBar,
    swiperSlide,
    swiper,
    Modal,
  },
};
</script>
<style lang="scss">
@import "./../assets/scss/mixin.scss";
@import "./../assets/scss/config.scss";
</style>