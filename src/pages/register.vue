<template>
  <div class="register">
    <div class="wrap">
      <a href="/#/index" class="logo">
        <img src="/imgs/logo-mi.png" alt />
      </a>
      <h4 class="title">注册小米帐号</h4>
      <div class="input">
        <input type="text" placeholder="请输入帐号要注册的用户名" v-model="username" />
      </div>
      <div class="input">
        <input type="password" placeholder="" v-model="password" />
      </div>
      <div class="btn-box"><a href="javascript:;" class="btn" @click="register">立即注册</a></div>
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
  name: 'register',
  data() {
    return {
      username: '',
      password: ''
    };
  },
  methods: {
    register() {
      let {username, password} = this;
      if (!password) return;
      this.axios.post('/user/register', {
        username,
        password,
        email: `${username}@163.com`
      }).then(() => {
        this.$message.success('注册成功');
        window.location.href = '/#/login';
      })
    }
  }
};
</script>


<style lang="scss">
@import "../assets/scss/config.scss";
@import "../assets/scss/mixin.scss";

.register {
  @include wh(100%, auto);
  min-height: 100%;
  background-color: $colorJ;
  overflow: hidden;

  .wrap {
    @include wh(854px, auto);
    margin: 30px auto;
    padding-bottom: 60px;
    background-color: $colorG;
    text-align: center;

    .logo {
      img {
        @include wh(49px, 49px);
      }
    }
    .title {
      font-size: 30px;
      font-weight: normal;
      margin-top: 40px;
      padding-bottom: 30px;
    }

    .input {
      margin: 0 auto;
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
        @include wh(240px, 42px);
        line-height: 42px;
      }
    }
  }

  .footer {
    height: 100px;
    padding-top: 60px;
    padding-bottom: 105px;
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