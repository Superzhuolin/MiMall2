<template>
<div class="order-confirm">order-confirm</div>
</template>
<script>
import OrderHeader from './../components/OrderHeader'
import Modal from "./../components/Modal";
export default {
  name: "order-confirm",
  data() {
    return {
      list: [], //收获地址列表
      cartList: [], //购物车需要结算的商品列表
      cartTotalPrice: 0, //商品总金额
      count: 0, //商品结算数量
      checkedItem: {}, //选中的商品状态
      userAction: "", //用户行为  0:新增  1:编辑  2:删除
      showDelModal:false,//是否显示删除弹框
      showEditModal: false, //是否显示删除弹框
      checkedIndex:0,//当前收货地址选中的索引
    };
  },
  components: {
    Modal,
    OrderHeader
  },
  mounted() {
    this.getAddressList();
    this.getCartList();
  },
  methods: {
    getAddressList() {
      this.axios.get("/shippings").then((res) => {
        //status=0时返回的是res.data  所以不用写res.data
        this.list = res.list; //获取地址列表中的数据
      });
    },//打开新增地址弹框
    openAddressModal(){
      this.userAction = 0;
      this.checkedItem = {};
      this.showEditModal = true;
    },//编辑地址弹框
    editAddressModal(item){
      this.userAction = 1;
      this.checkedItem = item;
      this.showEditModal = true;
    },
    delAddress(item) {
      this.checkedItem = item;
      this.userAction = 2;
      this.showDelModal = true;
    },
    // 地址删除/编辑/新增功能
    submitAddress() {
      let { checkedItem, userAction } = this; //对象解构语法
      let method, url,params={};
      if (userAction == 0) { //新增
        (method = "post"), (url = "/shippings");
        
      } else if (userAction == 1) {//编辑
        (method = "put"), (url = `/shippings/${checkedItem.id}`);
      } else { //删除
        (method = "delete"), (url = `/shippings/${checkedItem.id}`);
      }
      if(userAction == 0||userAction==1){
        let { receiverName, receiverMobile, receiverProvince, receiverCity, receiverDistrict, receiverAddress, receiverZip} = checkedItem;
        let errMsg="";
        if(!receiverName){
          errMsg="请输入收货人名称"
        }else if(!receiverMobile || !/\d{11}/.test(receiverMobile)){
          errMsg="请输入正确的手机号"
        }else if(!receiverProvince ){
          errMsg="请选择省份"
        }else if(!receiverCity ){
          errMsg="请选择对应的城市"
        }else if(!receiverAddress ||!receiverDistrict){
          errMsg="请输入收货地址"
        }else if(!/\d{6}/.test(receiverZip)){
          errMsg="请输入六位邮编"
        }
        if(errMsg){
          this.$message.error(errMsg);
          return;
        }
         params = {
          receiverName,
          receiverMobile,
          receiverProvince,
          receiverCity,
          receiverDistrict,
          receiverAddress,
          receiverZip
        }
      }
      this.axios[method](url,params).then(() => {
        this.closeModal();
        this.getAddressList();//防止不同账号数据不统一,需要重新拉数据
        this.$message.success("操作成功");
      });
    },
    closeModal() {
      this.checkedItem = {};
      this.userAction = "";
      this.showDelModal = false;
      this.showEditModal=false;
    },
    getCartList() {
      this.axios.get("/carts").then((res) => {
        let list = res.cartProductVoList; //获取购物车中所有商品的数据
        this.cartTotalPrice = res.cartTotalPrice; //商品中金额
        this.cartList = list.filter((item) => item.productSelected); //获取商品的选中状态
        this.cartList.map((item) => {
          this.count += item.quantity; //将购物车中每种商品的数量都加给count
        });
      });
    },//订单提交
    orderSubmit(){
      //找收货地址里面的索引  找不到就说明地址不存在
      let item = this.list[this.checkedIndex];
      if(!item){
        this.$message.error("请选择一个收货地址");
        return;
      }
      this.axios.post("/orders",{
        shippingId:item.id
      }).then((res)=>{
        this.$router.push({
          path:"/order/pay",
          query:{
            orderNo:res.orderNo
          }
        })
      })

    }
  },
};
</script>
<style lang="scss">
.order-confirm {
  .wrapper {
    background-color: #f5f5f5;
    padding-top: 30px;
    padding-bottom: 84px;
    .order-box {
      background-color: #ffffff;
      padding-left: 40px;
      padding-bottom: 40px;
      .addr-title {
        font-size: 20px;
        color: #333333;
        font-weight: 200;
        margin-bottom: 21px;
      }
      .item-address {
        padding-top: 38px;
        .addr-list {
          .addr-info,
          .addr-add {
            box-sizing: border-box;
            float: left;
            width: 271px;
            height: 180px;
            border: 1px solid #e5e5e5;
            margin-right: 15px;
            padding: 15px 24px;
            font-size: 14px;
            color: #757575;
          }
          .addr-info {
            cursor: pointer;
            h2 {
              height: 27px;
              font-size: 18px;
              font-weight: 300;
              color: #333;
              margin-bottom: 10px;
            }
            .street {
              height: 50px;
            }
            .action {
              height: 50px;
              line-height: 50px;
              .icon {
                width: 20px;
                height: 20px;
                fill: #666666;
                vertical-align: middle;
                &:hover {
                  fill: #ff6700;
                }
              }
            }
            &.checked {
              border: 1px solid #ff6700;
            }
          }
          .addr-add {
            text-align: center;
            color: #999999;
            cursor: pointer;
            .icon-add {
              width: 30px;
              height: 30px;
              border-radius: 50%;
              background: url("/public/imgs/icon-add.png") #e0e0e0 no-repeat
                center;
              background-size: 14px;
              margin: 0 auto;
              margin-top: 45px;
              margin-bottom: 10px;
            }
          }
        }
      }
      .item-good {
        margin-top: 34px;
        border-bottom: 1px solid #e5e5e5;
        padding-bottom: 12px;
        h2 {
          border-bottom: 1px solid #e5e5e5;
          padding-bottom: 5px;
        }
        li {
          display: flex;
          align-items: center;
          height: 40px;
          line-height: 40px;
          margin-top: 10px;
          font-size: 16px;
          color: #333333;
          .good-name {
            flex: 5;
            img {
              width: 30px;
              height: 30px;
              vertical-align: middle;
            }
          }
          .good-price {
            flex: 2;
          }
          .good-total {
            padding-right: 44px;
            color: #ff6600;
          }
        }
      }
      .item-shipping,
      .item-invoice {
        margin-top: 31px;
        line-height: 20px;
        h2 {
          display: inline-block;
          margin-right: 71px;
          font-size: 20px;
          width: 80px;
        }
        span,
        a {
          font-size: 16px;
          color: #ff6700;
          margin-right: 23px;
        }
      }
      .detail {
        padding: 50px 44px 33px 0;
        border-bottom: 1px solid #f5f5f5;
        text-align: right;
        font-size: 16px;
        color: #666666;
        .item-val {
          color: #ff6700;
        }
        .item {
          line-height: 15px;
          margin-bottom: 12px;
        }
        .item-val {
          display: inline-block;
          width: 100px;
        }
        .item-total {
          .item-val {
            font-size: 28px;
          }
        }
      }
      .btn-group {
        margin-top: 37px;
        text-align: right;
      }
    }
  }
  .edit-wrap{
      font-size:14px;
      .item{
        margin-bottom:15px;
        .input{
          display:inline-block;
          width:283px;
          height:40px;
          line-height:40px;
          padding-left:15px;
          border:1px solid #E5E5E5;
          &+.input{  //定义下一个元素的样式
            margin-left:14px;
          }
        }
        select{
          height:40px;
          line-height:40px;
          border:1px solid #E5E5E5;
          margin-right:15px;
        }
        textarea{
          height:62px;
          width:100%;
          padding:13px 15px;
          box-sizing:border-box;
          border:1px solid #E5E5E5;
        }
      }
    }
}
</style>