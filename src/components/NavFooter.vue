<template>
  <div class="footer">
    <div class="footer-logo">
      <img class="logo-icon" src="/imgs/logo-footer.png" alt="">
      <p class="logo-desc">小米商城</p>
    </div>
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
       <div class="declare">本站点只用于学习 不做任何商业用途</div>
    </div>
    
  </div>
</template>


<script>
export default {
  name: 'nav-footer'
}
</script>

<style lang="scss" scoped>
@import '../assets/scss/config.scss';
.footer {
  position: relative;
  height: 234px;
  background-color: $colorB;
  color: $colorD;
  border-top: 4px solid $colorA;
  font-size: $fontI;
  text-align: center;
  .footer-logo {
    margin-top: 46px;
    margin-bottom: 31px;
    .logo-icon {
      width: 53px;
      height: 36px;
      margin-bottom: 13px;
    }
  }

  .footer-link {
    margin-bottom: 13px;
    .f-link {
      color: $colorD;
      &:hover {
        color: $colorA;
      }
    }
    span {
      margin: 0 10px;
    }
  }

  .copyright {
    .c-src {
      color: $colorA;
    }
  }

  .declare {
    position: absolute;
    top: 50%;
    left: 50%;
    font-size: $fontC;
    opacity: .3;
    transform: translate(-50%, -50%);
  }
}

</style>