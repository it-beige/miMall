<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      res: {}
    }
  },
  mounted() {
    this.getUser();
    this.getCartCount();
  },
  methods: {
    // 获取用户信息
    getUser() {
      this.axios.get('/user').then((res = {}) => {
        this.$store.dispatch('saveUserName', res.username);
      })
    },
    // 获取购物车信息
    getCartCount() {
      this.axios.get('/carts/products/sum').then((res) => {
        this.$store.dispatch('saveCartCount', res);
      })
    }
  }
  
}
</script>

<style lang="scss">
@import './assets/scss/reset.scss';
@import './assets/scss/config.scss';
@import './assets/scss/mixin.scss';
@import './assets/scss/button.scss';
</style>
