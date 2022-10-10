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
            购物车
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
            <div class="children">
              <ul>
                <li class="product" >
                  <a href="" target="_blank">
                    <div class="pro-img">
                      <img src="https://cdn.cnbj0.fds.api.mi-img.com/b2c-mimall-media/f515ab05232ed14ccd78ec67e024495a.png" alt="item.subtitle" />
                    </div>
                    <div class="pro-name">小米CC9</div>
                    <div class="pro-price">1700元</div>
                  </a>
                </li>
                <li class="product" >
                  <a href="" target="_blank">
                    <div class="pro-img">
                      <img src="https://cdn.cnbj0.fds.api.mi-img.com/b2c-mimall-media/f515ab05232ed14ccd78ec67e024495a.png" alt="item.subtitle" />
                    </div>
                    <div class="pro-name">小米CC9</div>
                    <div class="pro-price">1700元</div>
                  </a>
                </li>
                <li class="product" >
                  <a href="" target="_blank">
                    <div class="pro-img">
                      <img src="https://cdn.cnbj0.fds.api.mi-img.com/b2c-mimall-media/f515ab05232ed14ccd78ec67e024495a.png" alt="item.subtitle" />
                    </div>
                    <div class="pro-name">小米CC9</div>
                    <div class="pro-price">1700元</div>
                  </a>
                </li>
                <li class="product" >
                  <a href="" target="_blank">
                    <div class="pro-img">
                      <img src="https://cdn.cnbj0.fds.api.mi-img.com/b2c-mimall-media/f515ab05232ed14ccd78ec67e024495a.png" alt="item.subtitle" />
                    </div>
                    <div class="pro-name">小米CC9</div>
                    <div class="pro-price">1700元</div>
                  </a>
                </li>
                <li class="product" >
                  <a href="" target="_blank">
                    <div class="pro-img">
                      <img src="https://cdn.cnbj0.fds.api.mi-img.com/b2c-mimall-media/f515ab05232ed14ccd78ec67e024495a.png" alt="item.subtitle" />
                    </div>
                    <div class="pro-name">小米CC9</div>
                    <div class="pro-price">1700元</div>
                  </a>
                </li>
                <li class="product" >
                  <a href="" target="_blank">
                    <div class="pro-img">
                      <img src="https://cdn.cnbj0.fds.api.mi-img.com/b2c-mimall-media/f515ab05232ed14ccd78ec67e024495a.png" alt="item.subtitle" />
                    </div>
                    <div class="pro-name">小米CC9</div>
                    <div class="pro-price">1700元</div>
                  </a>
                </li>
              </ul>
            </div>
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
@import "/src/assets/scss/base.scss";
@import "/src/assets/scss/mixin.scss";
@import "/src/assets/scss/config.scss";

.header {
  .nav-topbar {
    height: 39px;
    line-height: 39px;
    background-color: #333333;
    color: #b0b0b0;
    .container {
      @include flex();
      a {
        color: #b0b0b0;
        display: inline-block;
        margin-right: 17px;
      }
      .my-cart {
        width: 110px;
        background-color: #ff6600;
        text-align: center;
        color: #ffffff;
        .icon-cart {
          @include bgImg(16px,12px,"/public/imgs/icon-cart-checked.png");
          margin-right: 4px;
        }
      }
    }
  }
  .nav-header {
    .container {
      position: relative;
      height: 112px;
      position: relative;
      @include flex();
      /* 菜单栏 */
      .header-menu{
        display: inline-block;
        width: 643px;
        padding-left: 209px;
        .item-menu{
          display: inline-block;
          color: #333333;
          font-weight: bold;
          font-size: 16px;
          line-height: 112px;
          margin-right: 20px;
          span{
            cursor: pointer;
          }
          &:hover{
            color: $colorA;
            .children{
              height: 220px;
            }
          }
          .children{
            position: absolute;
            top: 112px;
            left: 0;
            height: 220px;
            width: 1226px;
            border-top: 1px solid  #e5e5e5;
            box-shadow: 0px 7px 6px 0px rgba(0, 0, 0, 0.11);
            z-index: 10;
            transition: height 0.5s; //控制高度做动画
            // background-color: #ffffff; //设置背景色为白色,避免被其他颜色覆盖
           
            .product{
              position: relative;
              float:left;
              width: 16.6%;
              height: 220px;
              font-size: 12px;
              line-height: 12px;
              text-align: center;
              a{
                display: inline-block;
                .pro-img{
                  height: 137px;
                  img{
                  width: auto;
                  height: 111px;
                  margin-top: 26px;
                  }
                }
                .pro-name{
                  font-weight: bold;
                  margin-top: 19px;
                  margin-bottom: 8px;
                  color:$colorB;
                }
                .pro-price{
                  color:$colorA;
                }
                &:before{
                content:"";
                position: absolute;
                top: 28px;
                right: 0;
                border-left:1px solid red ;
                height: 100px;
                width: 1px;
                }
                &:last-child:before{
                  display: none;
                }
              }
            }
          }
        }
        
      }
      /* 搜索框 */
      .header-search{
        width: 319px;
        .wrapper{
          height: 50px;
          border: 1px solid #e0e0e0;
          display: flex;
          align-items: center;
          input{
            border: none;
            box-sizing: border-box; //使padding和border不会在影响元素宽高
            border-right: 1px solid #e0e0e0;
            width: 264px;
            height: 50px;
            padding-left: 14px;
          }
          a {
            @include bgImg(18px, 18px, "/public/imgs/icon-search.png");
            margin-left: 17px;
          }
        }
      }
    }
  }
}
</style>
