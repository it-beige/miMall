<template>
  <div class="nav-bar" :class="{'isFixed':isCeiling}">
    <div class="container">
      <div class="pro-title">
        {{title}}
      </div>
      <div class="pro-param">
        <a href="" class="param-item">概述</a><span class="param-line">|</span>
        <a href="" class="param-item">参数</a><span class="param-line">|</span>
        <a href="" class="param-item">用户评价</a>
        <slot name="buy"></slot>
      </div>
      
    </div>
  </div>
</template>

<script>
export default {
  name: 'nav-bar',
  props: {
    title: String
  },
  data() {
    return {
      isCeiling: false,
    }
  },
  mounted() {
    window.addEventListener('scroll', this.ceiling);
  },
  methods: {
    ceiling() {
      let scrollTop = window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop;
      this.isCeiling = scrollTop > 152 ? true : false;
    }
  },
  destroyed() {
    window.removeEventListener('scroll', this.ceiling, false);
  }
}
</script>

<style lang="scss">
@import '../assets/scss/config.scss';
@import '../assets/scss/mixin.scss';

.nav-bar {
  @include hl(70px, 70px);
  @include bd();
  background-color: $colorG;
  .container {
    @include flex();
    .pro-title {
      font-size: $fontH;
      color: $colorB;
      font-weight: bold;
    }
    .pro-param {
      font-size: $fontJ;
      .param-item {
        color: $colorC;
        &:last-of-type {
        margin-right: 10px;
        }
      }
      .param-line {
        margin: 0 10px;
      }
    }

  }

  &.isFixed {
    @include position(fixed, 0);
    width: 100%;
    box-shadow: 0 5px 5px $colorE;
  }
  
}


</style>