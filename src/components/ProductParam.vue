// 产品吸顶栏
<template>
  <!-- 动态绑定变量 若isFixed为true加上is_fixed类 -->
  <div class="nav-bar" :class="{ is_fixed: isFixed }">
    <div class="container">
      <!-- 标题栏 -->
      <div class="pro-title">小米8</div>
      <!-- 参数栏 -->
      <div class="pro-param">
        <a href="javasrcipt:;">概述</a><span>|</span>
        <a href="javasrcipt:;">参数</a><span>|</span>
        <a href="javasrcipt:;">用户评价</a>
        <!-- 插槽(button) -->
        <slot name="buy"></slot>
      </div>
    </div>
  </div>
</template>
 
<script>
export default {
  name: "nav-barr",
  data() {
    return {
      isFixed: false,
    };
  },
  props:{
    title:String
  },
  mounted() {
  },
  methods: {
  },
};
</script>
<style lang="scss">
@import "./../assets/scss/mixin.scss";
@import "./../assets/scss/config.scss";
.nav-bar{
  height: 70px;
  line-height: 70px;
  border: 1px solid $colorH;
  .container{
    @include flex();
    .pro-title{
      color: $colorB;
      font-size: $fontH;
      font-weight: bold;
    }
    .pro-param{
      font-size: $fontJ;
      a{
        color: $colorC;
      }
      span{
        margin: 0 10px;
      }
    }
  }
}
</style>
