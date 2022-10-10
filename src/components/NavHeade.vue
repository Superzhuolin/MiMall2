<template>
  <div class="header">
    <!-- 顶部栏 -->
    <div class="nav-topbar">
      <div class="container">
        <!-- 左边栏 -->
        <div class="topbar-menu">
          <a href="javascript:;">小米商城</a>
          <a href="javascript:;">MUI</a>
          <a href="javascript:;">云服务</a>
          <a href="javascript:;">协议规则</a>
        </div>
        <!-- 右边栏:登录  订单 -->
        <div class="topbar-user">
          <!-- <a href="javascript:;" >{{ username }}</a> -->
          <!-- <a href="/#/order/list">我的订单</a> -->
          <a href="javascript:;">登录</a>
          <a href="javascript:;">退出</a>
          <a href="javascript:;" class="my-cart">
            <!-- 购物车图标 -->
            <span class="icon-cart"></span>
            购物车({{ cartCount }})
          </a>
        </div>
      </div>
    </div>
    <!-- 导航栏 -->
    <div class="nav-header">
      <div class="container">
        <!-- logo -->
        <div class="header-logo">
          <a href="/#/index"></a>
        </div>
        <div class="header-menu">
          <!-- 小米手机 -->
          <div class="item-menu">
            <span>小米手机</span>
            <div class="children"></div>
          </div>
          <!-- RemMi红米手机 -->
          <div class="item-menu">
            <span>RemMi红米手机</span>
            <div class="children"></div>
          </div>
          <!-- 电视 -->
          <div class="item-menu">
            <span>电视</span>
            <div class="children">
            </div>
          </div>
        </div>
        <div class="header-search">
          <div class="wrapper">
            <input type="text" name="keyword" />
            <a href="javascript:;"></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
export default {
  name: "nav-header",
  data() {
    return {
      phoneList: [],
    };
  },
};
</script> 
<style lang="scss">
// @import "/src/assets/scss/base.scss";
// @import "/src/assets/scss/mixin.scss";
// @import "/src/assets/scss/config.scss";

.header {
  .nav-topbar {
    height: 39px;
    line-height: 39px;
    background-color: #333333;
    color: #b0b0b0;
    .container {
      width: 1226px;
      margin-right: auto;
      margin-left: auto;
      display: flex;
      justify-content: space-between;
      align-items: center;
      a {
        color: #b0b0b0;
        display: inline-block;
        margin-right: 17px;
      }
      .my-cart{
         width: 110px;
         background-color: #ff6600;
         text-align: center;
         color: #ffffff;
         .icon-cart{
          display: inline-block;
          width: 16px;
          height:12px;
          background: url("/public/imgs/icon-cart-checked.png") no-repeat center;
          background-size: contain;//等比缩放(会留白边)
          margin-right: 4px;
         }
      }
    }
  }
}
</style>
