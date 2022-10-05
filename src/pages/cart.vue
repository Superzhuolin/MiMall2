<template>
<div class="cart">cart</div>
</template>
<script>
import OrderHeader from "./../components/OrderHeader.vue";
import NavFooter from "./../components/NavFooter.vue";
import ServiceBar from "./../components/ServiceBar";
// import {Message} from 'element-ui';
export default {
  name: "cart",
  components: {
    OrderHeader,
    NavFooter,
    ServiceBar,
  },
  data() {
    return {
      list: [], //商品列表
      allChecked: false, //是否全选
      cartTotalPrice: 0, //商品总金额
      checkedNum: 0, //选中商品数量
    };
  },
  mounted() {
    this.getCartList();
  },
  methods: {
    // 获取购物车列表
    getCartList() {
      this.axios.get("/carts").then((res) => {
        this.renderData(res);
      });
    },//更新购物车数量和单选状态
    updataCart(item,type){
      let quantity = item.quantity,
          selected = item.productSelected;
      if(type == '-'){
          if(quantity <=1){
            // Message.warning("商品至少为一件");
            this.$message.warning("商品至少为一件");
            return;
          }
          --quantity;
      }else if(type == "+"){ 
         if(quantity >=item.productStock){
            // Message.warning("商品购买数量不能超过库存数量");
            this.$message.warning("商品购买数量不能超过库存数量");
            return;
          }
          ++quantity;
      }else{
        selected= !item.productSelected;// 单选
      }//更新商品信息
      this.axios.put(`/carts/${item.productId}`,{quantity,selected}).then((res)=>{
        this.renderData(res);
      })
    },//删除功能
    delProduct(item){
      this.axios.delete(`/carts/${item.productId}`).then((res)=>{
        // Message.success("删除成功");
        this.$message.success("删除成功");//全局插件用法
        this.renderData(res);
      })
    },
    //控制全选功能
    toggleAll() { 
      let url = this.allChecked ? "/carts/unSelectAll" : "/carts/selectAll";
      this.axios.put(url).then((res) => {
        this.renderData(res);
      });
    },
    // 公共赋值
    renderData(res) {
      this.list = res.cartProductVoList || [];
      this.allChecked = res.selectedAll;
      this.cartTotalPrice = res.cartTotalPrice;
      this.checkedNum = this.list.filter((item) => item.productSelected).length;// 过滤商品
    },
    // 购物车下单
    order(){
      let isCheck = this.list.every(item=>!item.productSelected);// 购物车是否全选
      if(isCheck){
        Message.warning("请选择一件商品");
      }else{
        this.$router.push("/order/confirm");//跳转到订单确定页面 
      }
    }
  },
};
</script>
<style lang="scss">
.cart {
  .wrapper {
    background-color: #f5f5f5;
    padding-top: 30px;
    padding-bottom: 114px;
    .cart-box {
      background-color: #fff;
      font-size: 14px;
      color: #999999;
      text-align: center;
      .checkbox {
        display: inline-block;
        width: 22px;
        height: 22px;
        border: 1px solid #e5e5e5;
        vertical-align: middle;
        margin-right: 17px;
        cursor: pointer;
        &.checked {
          background: url("/public/imgs/icon-gou.png") #ff6600 no-repeat center;
          background-size: 16px 12px;
          border: none;
        }
      }
      .cart-item-head {
        display: flex;
        height: 79px;
        line-height: 79px;
        .col-1 {
          flex: 1;
        }
        .col-2 {
          flex: 2;
        }
        .col-3 {
          flex: 3;
        }
      }
      .cart-item-list {
        .cart-item {
          display: flex;
          align-items: center;
          height: 125px;
          border-top: 1px solid #e5e5e5;
          font-size: 16px;
          .item-check {
            flex: 1;
          }
          .item-name {
            flex: 3;
            font-size: 18px;
            color: #333333;
            display: flex;
            align-items: center;
            img {
              width: 80px;
              height: 80px;
              vertical-align: middle;
            }
            span {
              margin-left: 30px;
            }
          }
          .item-price {
            flex: 1;
            color: #333333;
          }
          .item-num {
            flex: 2;
            .num-box {
              display: inline-block;
              width: 150px;
              height: 40px;
              line-height: 40px;
              border: 1px solid #e5e5e5;
              font-size: 14px;
              a {
                display: inline-block;
                width: 50px;
                color: #333333;
              }
              span {
                display: inline-block;
                width: 50px;
                color: #333333;
              }
            }
          }
          .item-total {
            flex: 1;
            color: #ff6600;
          }
          .item-del {
            flex: 1;
            width: 14px;
            height: 12px;
            background: url("/public/imgs/icon-close.png") no-repeat center;
            background-size: contain;
            cursor: pointer;
          }
        }
      }
    }
    .order-wrap {
      font-size: 14px;
      color: #666666;
      margin-top: 20px;
      height: 50px;
      line-height: 50px;
      .cart-tip {
        margin-left: 29px;
        a {
          color: #666666;
          margin-right: 37px;
        }
        span {
          color: #ff6600;
          margin: 0 5px;
        }
      }
      .total {
        font-size: 14px;
        color: #ff6600;
        span {
          font-size: 24px;
        }
        a {
          width: 202px;
          height: 50px;
          line-height: 50px;
          font-size: 18px;
          margin-left: 37px;
        }
      }
    }
  }
}
</style>