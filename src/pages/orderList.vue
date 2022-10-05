<template>
<div class="order-list">order-list</div>
</template>
<script>
  import OrderHeader from './../components/OrderHeader'
  import Loading from "./../components/Loading.vue"
  import NoData from "./../components/NoData.vue"
  import {Pagination,Button} from "element-ui";
  import infiniteScroll from "vue-infinite-scroll";
  export default{
    name:'order-list',
    components:{
      OrderHeader,
      Loading,
      NoData,
      [Pagination.name]:Pagination,
      [Button.name]:Button
    },
    directives:{infiniteScroll}, //配置
    data(){
      return{
        loading:false,//默认显示,数据回来时关闭
        list:[],
        pageSize:10,//一页十条
        pageNum:1,//当前页数
        total:0,
        showNextPage:true,//加载更多:是否显示按钮
        busy:false,//滚动加载是否触发
      }
    },
    mounted(){
      this.getOrderList();
    },
    methods:{
      getOrderList(){
        this.loading=true;
        this.busy=true; //bug:首次就会加载第二页
        this.axios.get("/orders",{
          params:{
            pageSize:10,//设置订单展示两条数据
            pageNum:this.pageNum,
          }
        }).then((res)=>{
          this.loading=false;
          // this.list=[]||res.list;
          this.list=this.list.concat(res.list);//拼接原数组从而实现加载更多
          this.total=res.total;
          this.showNextPage=res.hasNextPage;
          this.busy=false; 
        }).catch(()=>{
          this.loading=false;
        })
      },
      goPay(orderNo){
        // this.$router.push("/order/pay")   //1.字符串方式
       /*  this.$router.push({        //2.params传参方式  不可以把参数添加到地址栏
          name:'order-pay',
          params:{
            orderNo
          }
        }) */
        this.$router.push({   //3.query传参方式  可以把参数添加到地址栏
          path:'/order/pay',
          query:{
            orderNo
          }
        })
      },//第一种方法:分页器
      handleChange(pageNum){
        this.pageNum=pageNum;
        this.getOrderList();
      },//第二种方法:加载更多按钮
      loadMore(){
        this.pageNum++;
        this.getOrderList();
      },//第三种方法:滚动加载,通过npm插件实现
      scrollMore(){
        this.busy=true;//禁止滚动
        setTimeout(()=>{
        this.pageNum++;
        this.getList();
        },500);
      },//专门给滚动加载使用
      getList(){
        this.loading=true;//请求开始,加载图片显示
        this.axios.get("/orders",{
          params:{
            pageSize:10,//设置订单展示数据数量
            pageNum:this.pageNum,
          }
        }).then((res)=>{
          this.list=this.list.concat(res.list);//拼接原数组从而实现加载更多
          this.loading=true;//请求结束,图片不加载
          if(res.hasNextPage){
            this.busy=false;//开启滚动
          }else{
            this.busy=true;//禁止滚动
          }
        })
      },
    }
  }
</script>
<style lang="scss">
  @import './../assets/scss/config.scss';
  @import './../assets/scss/mixin.scss';
  .order-list{
    .wrapper{
      background-color:$colorJ;
      padding-top:33px;
      padding-bottom:110px;
      .order-box{
        .order{
          @include border();
          background-color:$colorG;
          margin-bottom:31px;
          &:last-child{
            margin-bottom:0;
          }
          .order-title{
            @include height(74px);
            background-color:$colorK;
            padding:0 43px;
            font-size:16px;
            color:$colorC;
            .item-info{
              span{
                margin:0 9px;
              }
            }
            .money{
              font-size:26px;
              color:$colorB;
            }
          }
          .order-content{
            padding:0 43px;
            .good-box{
              width:88%;
              .good-list{
                display: flex;
                align-items: center;
                height:145px;
                .good-img{
                  width:112px;
                  img{
                    width:100%;
                  }
                }
                .good-name{
                  font-size:20px;
                  color:$colorB;
                }
              }
            }
            .good-state{
              @include height(145px);
              font-size: 20px;
              color:$colorA;
              a{
                color:$colorA;
              }
            }
          }
        }
        .pagination{
          text-align:right;
        }
        .el-pagination.is-background .el-pager li:not(.disabled).active{
          background-color: #FF6600;
        }
        .el-button--primary{
          background-color: #FF6600;
          border-color: #FF6600;
        }
        .load-more,.scroll-more{
          text-align:center;
        }
      }
    }
  }
</style>