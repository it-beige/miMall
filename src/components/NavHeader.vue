<template>
  <div class="header">
    <div class="nav-topbar">
      <div class="container">
        <div class="menu">
          <a class="menu-a" href="http://www.beige.world">小米商城</a>
          <a class="menu-a" href="http://www.beige.world">MIUI</a>
          <a class="menu-a" href="http://www.beige.world">云服务</a>
          <a class="menu-a" href="http://www.beige.world">协议规则</a>
        </div>
        <div class="user">
          <a class="menu-a" href="javascript:;" v-if="username">{{username}}</a>
          <a class="menu-a" href="javascript:;" v-if="!username" @click="login">登录</a>
          <a class="menu-a" href="javascript:;" v-if="username">我的订单</a>
          <a class="menu-a my-cart" href="javascript:;" @click="goToCart">
            <span class="icon-cart"></span>
            购物车({{cartCount}})
          </a>
        </div>
      </div>
    </div>
    <div class="nav-header">
      <div class="container">
        <div class="header-logo">
          <a href="/#/index" class="logo-icon"></a>
        </div>
        <div class="header-menu">
          <div class="item-menu">
            <span>小米手机</span>
            <div class="children">
              <ul>
                <li class="product" v-for="(item, index) in phoneList" :key="index">
                  <a class="product-wrapper" :href="`/#/product/${item.id}`" target="_blank">
                    <div class="pro-img">
                      <img
                        class="img"
                        v-lazy="item.mainImage"
                        :alt="item.subtitle"
                      />
                    </div>
                    <div class="pro-name">{{item.name}}</div>
                    <div class="pro-price">{{item.price | currency}}</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <div class="item-menu">
            <span>笔记本</span>
            <div class="children">
              <ul>
                <li class="product" v-for="(item, index) in jotterList" :key="index">
                  <a class="product-wrapper" href="`/#/index" target="_blank">
                    <div class="pro-img">
                      <img
                        class="img"
                        v-lazy="item.mainImage"
                        :alt="item.name"
                      />
                    </div>
                    <div class="pro-name">{{item.name}}</div>
                    <div class="pro-price">{{item.price}}</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
          <div class="item-menu">
            <span>电视</span>
             <div class="children">
              <ul>
                <li class="product" v-for="(item, index) in televisionList" :key="index">
                  <a class="product-wrapper" href="`/#/index" target="_blank">
                    <div class="pro-img">
                      <img
                        class="img"
                        v-lazy="item.mainImage"
                        :alt="item.name"
                      />
                    </div>
                    <div class="pro-name">{{item.name}}</div>
                    <div class="pro-price">{{item.price}}</div>
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
        <div class="header-search">
          <div class="wrapper">
            <input class="search-input" type="text" name="keyword" />
            <a class="search-icon" href="javascript:;"></a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import { mapState } from 'vuex';
export default {
  name: "nav-header",
  data() {
    return {
      phoneList: [],
      televisionList: [
        {
          mainImage: '/imgs/nav-img/nav-3-1.jpg',
          name: '小米壁画电视 65英寸',
          price: '699元'
        },
        {
          mainImage: '/imgs/nav-img/nav-3-2.jpg',
          name: '小米全面屏电视E55A',
          price: '1999元'
        },
        {
          mainImage: '/imgs/nav-img/nav-3-3.png',
          name: '小米电视4A 32英寸',
          price: '8999元'
        },
        {
          mainImage: '/imgs/nav-img/nav-3-4.jpg',
          name: 'Redmi 智能电视 MAX 98',
          price: '19999元'
        },
        {
          mainImage: '/imgs/nav-img/nav-3-5.jpg',
          name: 'Redmi 红米电视 70英寸 R70A',
          price: '3099元'
        },
        {
          mainImage: '/imgs/nav-img/nav-3-6.png',
          name: '小米电视4A 65英寸',
          price: '6999元'
        },
      ],
      jotterList: [
        {
          mainImage: '/imgs/nav-img/nav-6-1.webp',
          name: 'RedmiBook 13',
          price: '4199元起'
        },
        {
          mainImage: '/imgs/nav-img/nav-6-2.png',
          name: '小米笔记本Pro 15',
          price: '5499元起'
        },
        {
          mainImage: '/imgs/nav-img/nav-6-3.webp',
          name: 'RedmiBook 14',
          price: '3999元起'
        },
        {
          mainImage: '/imgs/nav-img/nav-6-4.webp',
          name: '游戏本2020款',
          price: '6999元起'
        },
        {
          mainImage: '/imgs/nav-img/nav-6-5.png',
          name: '小米笔记本 15.6"',
          price: '3899元起'
        },
         {
          mainImage: '/imgs/nav-img/nav-6-6.png',
          name: '小米笔记本Air 12.5"',
          price: '3299元起'
        }
      ]
    }
  },
  computed: {
    ...mapState(['username', 'cartCount'])
  },
  filters: {
    currency(val) {
      if (!val) return '0.00';
      return `￥${val.toFixed(2)}元`;
    }
  },
  mounted() {
    this.getProductList();
  },
  methods: {
    // 动态获取产品信息
    getProductList() {
      this.axios.get('/products', {
        params: {
          categoryId: '100012',
          pageSize: 6,
        }
      }).then((res) => {
        this.phoneList = res.list;
      })
    },
    // 跳转到我的购物车
    goToCart() {
      this.$router.push('/cart');
    },
    // 登录跳转
    login() {
      this.$router.push('/login');
    }
  }
};
</script>

<style lang="scss">
@import "../assets/scss/base.scss";
@import "../assets/scss/config.scss";
@import "../assets/scss/mixin.scss";
.header {
  .nav-topbar {
    height: 39px;
    line-height: 39px;
    color: #b0b0b0;
    background-color: #333;
    .container {
      @include flex();
      .menu-a {
        display: inline-block;
        color: #b0b0b0;
        margin-right: 17px;
        text-align: center;
      }
      // 我的购物车
      .my-cart {
        width: 110px;
        background-color: #f60;
        margin-right: 0;
        color: #fff;
        // 图标
        .icon-cart {
          @include bgImg(16px, 12px, "/imgs/icon-cart-checked.png");
          margin-right: 4px;
        }
      }
    }
  }

  .nav-header {
    .container {
      position: relative;
      height: 112px;
      @include flex();
     

      .header-menu {
        display: inline-block;
        width: 643px;
        padding-left: 209px;
        .item-menu {
          line-height: 112px;
          display: inline-block;
          color: #333;
          font-weight: bold;
          font-size: 17px;
          margin-right: 20px;
          cursor: pointer;
          
          &:hover {
            color: $colorA;
            .children {
              height: 220px;
              opacity: 1;
              border: 1px solid $colorH;
            }
          }

          .children {
            z-index: 10;
            width: 1226px;
            height: 0;
            opacity: 0;
            position: absolute;
            top: 112px;
            left: 0;
            box-shadow: 0 7px 6px 0 rgba(0,0,0,.11);
            transition: all 0.5s;
            background-color: $colorG;
            overflow: hidden;
            .product {
              position: relative;
              float: left;
              width: 16.6%;
              height: 220px;
              font-size: 12px;
              line-height: 12px;
              text-align: center;
              &::after {
                content: '';
                position: absolute;
                top: 28px;
                right: 0;
                width: 1px;
                height: 100px;
                border-right: 1px solid $colorF;
              }
              &:last-child::after {
                border: none;
              }
              .product-wrapper {
                display: inline-block;
                .pro-img {
                  height: 137px;
                  .img {
                    margin-top: 27px;
                    width: auto;
                    height: 110px;
                  }
                }
                .pro-name {
                  color: $colorB;
                  margin-top: 19px;
                  margin-bottom: 8px;
                  font-weight: 700;
                }

                .pro-price {
                  color: $colorA;
                }
              }
            }
          }
        }
      }

      .header-search {
        width: 319px;
        .wrapper {
          border: 1px solid #e0e0e0;
          height: 50px;
          display: flex;
          align-items: center;
          .search-input {
            border: none;
            border-right: 1px solid #e0e0e0;
            width: 264px;
            box-sizing: border-box;
            height: 50px;
            padding-left: 14px;
          }

          .search-icon {
            @include bgImg(18px, 18px, "/imgs/icon-search.png");
            margin-left: 17px;
          }
        }
      }
    }
  }
}
</style>