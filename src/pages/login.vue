<template>
<div class="login">login</div>

</template>
<script>
import { mapActions } from "vuex"; //从vuex中解构mapActions对象
// import {Message} from 'element-ui';
export default {
  name: "login",
  data() {
    return {
      username: "",
      password: "",
      userId: "", //前后端分离,使用userId作为cookie身份凭证
    };
  },
  methods: {
    login() {
      let { username, password } = this; //ES6中的对象解构
      //调用接口  POST /user/login
      this.axios
        .post("/user/login", {
          username,
          password, //传参 简写
        })
        .then((res) => {
          // this.$cookie.set("userId", res.id, { expires: "1M" }); //设置用户ID
          this.$cookie.set("userId", res.id, { expires: "Session" }); //设置用户ID

          /*  登录时通过dispatch派发action行为saveUserName,action行为会提交commit到
         mutation,mutation会自动提交到state状态里面去做出改变.从而状态会重新重新渲染视图. */
          // this.$store.dispatch("saveUserName",res.username);//读取后,保存用户名
          this.saveUserName(res.username);
          // this.$router.push("/index"); //回到首页
          this.$router.push({
            // path:"/index",
            // query:{
            //   from:"login"
            // }
            name:"index",
            params:{
              from:"login"
            }
          }); //回到首页
        });
    },
    ...mapActions(["saveUserName"]),
    register() {
      this.axios
        .post("/user/login", {
          username: "admin1",
          password: "admin1",
          email: "amin1@163.com",
        })
        .then(() => {
          // Message.success("注册成功");
          this.$message.success("注册成功");
        });
    },
  },
};
</script>
<style lang="scss">
.login {
  & > .container {
    height: 113px;
    img {
      width: auto;
      height: 100%;
    }
  }
  .wrapper {
    background: url("/public/imgs/login-bg.jpg") no-repeat center;
    .container {
      height: 576px;
      .login-form {
        box-sizing: border-box;
        padding-left: 31px;
        padding-right: 31px;
        width: 410px;
        height: 510px;
        background-color: #ffffff;
        position: absolute;
        bottom: 29px;
        right: 0;
        h3 {
          line-height: 23px;
          font-size: 24px;
          text-align: center;
          margin: 40px auto 49px;
          .checked {
            color: #ff6600;
          }
          .sep-line {
            margin: 0 32px;
          }
        }
        .input {
          display: inline-block;
          width: 348px;
          height: 50px;
          border: 1px solid #e5e5e5;
          margin-bottom: 20px;
          input {
            width: 100%;
            height: 100%;
            border: none;
            padding: 18px;
          }
        }
        .btn {
          width: 100%;
          line-height: 50px;
          margin-top: 10px;
          font-size: 16px;
        }
        .tips {
          margin-top: 14px;
          display: flex;
          justify-content: space-between;
          font-size: 14px;
          cursor: pointer;
          .sms {
            color: #ff6600;
          }
          .reg {
            color: #999999;
            span {
              margin: 0 7px;
            }
          }
        }
      }
    }
  }
  .footer {
    height: 100px;
    padding-top: 60px;
    color: #999999;
    font-size: 16px;
    text-align: center;
    .footer-link {
      a {
        color: #999999;
        display: inline-block;
      }
      span {
        margin: 0 10px;
      }
    }
    .copyright {
      margin-top: 13px;
    }
  }
}
</style>