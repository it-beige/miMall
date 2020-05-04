<template>
  <div class="login">
    <div class="container">
      <a href="/#/index" class="logo">
        <img class="logo-img" src="/imgs/login-logo.png" />
      </a>
    </div>
    <div class="wrapper">
      <div class="container">
        <div class="login-form">
          <h3 class="account-mtdhods">
            <span class="account">帐号登录</span>
            <span class="spline">|</span>
            <span>扫码登录</span>
          </h3>
          <div class="input"><input type="text" placeholder="请输入帐号" v-model="username"></div>
          <div class="input"><input type="text" placeholder="请输入密码" v-model="password"></div>
          <div class="btn-box"><a href="javascript:;" class="btn" @click="login">登录</a></div>
          <div class="tips">
            <div class="sms">手机短信登录/<a class="register" href="/#/register">注册</a></div>
            <div class="reg">立即注册<span>|</span>忘记密码？</div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">
      <div class="footer-link">
        <a class="f-link" href="http://www.beige.world" target="_blank">北歌的个人博客</a><span>|</span>
        <a class="f-link" href="https://juejin.im/user/5d63054ae51d453c11684c84" target="_blank">北歌的掘金</a><span>|</span>
        <a class="f-link" href="javascript:;" target="_blank">北歌的公众号(beige61)</a><span>|</span>
        <a class="f-link" href="javascript:;" target="_blank">后台管理系统项目</a>
      </div>
      <div class="copyright">
          Copyright ©2020
          <a class="c-src" href="http://www.mimall.beige.world">www.mimall.beige.world</a>
          All Rights Reserved.
        </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
      userId: '',
      res: {}
    };
  },
  methods: {
    login() {
      let {
        username,
        password,
      } = this;
      this.axios.post('/user/login', {
        username,
        password
      }).then((res) => {
        this.$cookie.set('userId', res.id, {expires: '1M'});
        // todo 保存用户信息
        this.$router.push('/index');
      })
    }
  }
};
</script>

<style lang="scss">
@import '../assets/scss/config.scss';
@import '../assets/scss/mixin.scss';
.login {
  .logo {
    display: inline-block;
    .logo-img {
      width: auto;
      height: 100%;
    }
  }

  .wrapper {
    background: url('/imgs/login-bg.jpg') no-repeat center;

    .container {
      height: 576px;
      position: relative;

      .login-form {
        box-sizing: border-box;
        @include positionR(absolute, 29px, 0);
        @include wh(410px, 510px);
        padding: 0 31px;
        background-color: $colorG;

        .account-mtdhods {
          font-size: 24px;
          line-height: 24px;
          text-align: center;
          margin: 40px auto 29px;
          .account {
            color: $colorA;
          }
          .spline {
            margin: 0 32px;
            font-size: 26px;
          }
        }

        .input {
          @include wh(348px, 50px);
          @include bd();
          margin-bottom: 20px;
          input {
            @include wh(100%, 100%);
            border: none;
            padding-left: 18px;
          }
        }

        .btn-box {
          .btn {
            width: 100%;
            line-height: 50px;
            font-size: $fontI;
          }
        }

        .tips {
          @include flex();
          margin-top: 14px;
          font-size: $fontJ;
          cursor: pointer;
          .sms {
            color: $colorA;
            .register {
              color: $colorA;
            }
          }

          .reg {
            color: $colorD;
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
    color: $colorD;
    font-size: $fontI;
    text-align: center;
    .footer-link {
      .f-link {
        display: inline-block;
        color: $colorD;
      }
      span {
        margin: 0 10px;
      }
    }

    .copyright {
      margin-top: 13px;
      .c-src {
        color: $colorA;
      }
    }
  }
}
</style>