<template>
  <div class="order-header">
    <div class="container clearfix">
        <div class="header-logo fl">
          <a href="/#/index" class="logo-icon"></a>
        </div>
        <div class="title fl">
          <h2>{{title}}<slot name="tip"></slot></h2>
        </div>
        <div class="fr">
          <a href="javascript:;" class="username">{{username}}</a>
        </div>
      </div>
  </div>
</template>


<script>
import { mapState } from 'vuex';
export default {
  name: 'order-header',
  data() {
    return {

    }
  },
  props: {
    title: String
  },
  computed: {
    ...mapState(['username'])
  }
}
</script>

<style lang="scss">
@import '../assets/scss/config.scss';
@import '../assets/scss/mixin.scss';
  .order-header {
    padding: 30px 0;
    border-bottom: 2px solid $colorA;
    @include hl(55px, 55px);
    .container {
      .title {
        margin-left: 54px;
        h2 {
          font-size: 28px;
          color: #333;

          span {
            font-size: 14px;
            margin-left: 17px;
            color: #999;
            font-weight: 200;
          }
        }
      }

      .username {
        color: #666;
        font-size: 16px;
      }
    }
  }
</style>