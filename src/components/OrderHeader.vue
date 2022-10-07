// 购物车头部组件
<template>
  <div class="order-header">
    order-header
  </div>
</template>

<script>
import { mapState } from "vuex";

export default {
  name: "order-header",
  props:{
    // 子组件接受父组件传递过的值
    title:String,
  },
    computed: {
    ...mapState(["username"]),
  },
};
//
</script>
<style  lang="scss">
.order-header{
  padding: 30px 0;
  border-bottom: 2px solid #ff6600;
  .header-logo{
    float: left;
  }
  .title,.username{
    display: inline-block;
    height: 55px;
    line-height: 55px;
  }
  .title{
    float: left;
    margin-left: 54px;
    h2{
      font-size: 28px;
      color: #333333;
    }
    span{
      font-size: 14px;
      margin-left: 17px;
      color: #999999;
      font-weight: 200;
    }
  }
  .username{
    float: right;
    a{
      color: #666666;
      font-size: 16px;
    }  
  }
}
</style>>

