<template>
  <div class="detail">detail</div>
</template>
<script>
import { swiper, swiperSlide } from "vue-awesome-swiper";
import ProductParam from "./../components/ProductParam";
import ServiceBar from "./../components/ServiceBar";
export default {
  name: "detail",
  data() {
    return {
      id: this.$route.params.id, //获取商品ID
      err: "",
      version: 1, //商品版本切换
      product: {}, //商品信息
      swiperOption: {
        autoplay: true,
        pagination: {
          el: ".swiper-pagination",
          clickable: true,
        },
      },
    };
  },
  components: {
    swiper,
    swiperSlide,
    ProductParam,
    ServiceBar,
  },
};
</script>
<style lang="scss">
@import "./../assets/scss/config.scss";
@import "./../assets/scss/mixin.scss";
</style>