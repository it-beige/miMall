<template>
  <div class="index">
    <div class="container">
      <div class="swiper-box">
        <div class="nav-menu">
          <ul class="menu-wrap">
            <li class="menu-item">
              <a class="item-name" href="javascript:;">手机 电话卡</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="menu-item">
              <a class="item-name" href="javascript:;">电视 盒子</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="menu-item">
              <a class="item-name" href="javascript:;">笔记本 平板</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="menu-item">
              <a class="item-name" href="javascript:;">家电 插线板</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="menu-item">
              <a class="item-name" href="javascript:;">出行 穿戴</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="menu-item">
              <a class="item-name" href="javascript:;">智能 路由器</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="menu-item">
              <a class="item-name" href="javascript:;">电源 配件</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
            <li class="menu-item">
              <a class="item-name" href="javascript:;">生活 箱包</a>
              <div class="children">
                <ul v-for="(item, index) in menuList" :key="index">
                  <li v-for="(subItem, index) in item" :key="index">
                    <a :href="`${subItem ? `/#/product${subItem.id}` : 'javascript:;'}`">
                      <img :src="`${subItem ? subItem.img : 'imgs/item-box-1.png'}`" alt />
                      {{`${subItem ? subItem.name : '小米'}`}}
                    </a>
                  </li>
                </ul>
              </div>
            </li>
          </ul>
        </div>
        <swiper :options="swiperOption">
          <swiper-slide v-for="(item, index) in slideList" :key="index">
            <a :href="`/#/product/${item.id}`">
              <img v-lazy="item.img" />
            </a>
          </swiper-slide>
          <!-- 分页器 -->
          <div class="swiper-pagination" slot="pagination"></div>
          <!-- 导航按钮 -->
          <div class="swiper-button-prev" slot="button-prev"></div>
          <div class="swiper-button-next" slot="button-next"></div>
        </swiper>
      </div>
      <div class="ads-box">
        <a
          class="ads-item"
          :href="`/#/product/${item.id}`"
          v-for="(item, index) in adsList"
          :key="index"
        >
          <img v-lazy="item.img" alt />
        </a>
      </div>
      <div class="banner">
        <a href="/#/product/30">
          <img v-lazy="`/imgs/banner-1.png`" alt />
        </a>
      </div>
    </div>
    <div class="product-box">
        <div class="container">
          <h2 class="pro-phone">手机</h2>
          <div class="wrapper">
            <div class="banner-left">
              <a href="/#/product/35">
                <img class="b-img" v-lazy="'/imgs/mix-alpha.jpg'" alt />
              </a>
            </div>
            <div class="list-box">
              <div class="list" v-for="(arr, i) in phoneList" :key="i">
                <div class="item" v-for="(item, j) in arr" :key="j">
                  <span :class="{'product newProduct' : j % 2 == 0}">新品</span>
                  <div>
                    <img class="item-img" v-lazy="item.mainImage" alt />
                  </div>
                  <div class="item-info">
                    <h3 class="info-name">{{item.name}}</h3>
                    <p class="info-desc">{{item.subtitle}}</p>
                    <p class="info-price" @click="addCart(item.id)">{{item.price}}元</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    <service-bar></service-bar>
    <modal 
    title="提示" 
    sureText="查看购物车"
    btnType='1'
    modalType="middle"
    :showModal="showModal"
    @submit="goToCart"
    @cancel="showModal = false"
    >
    <template v-slot:body>
      <p>商品添加成功！</p>
    </template>
    </modal>
  </div>
</template>


<script>
import ServiceBar from "../components/ServiceBar";
import Modal from "../components/Modal";
import { swiper, swiperSlide } from "vue-awesome-swiper";
import "swiper/dist/css/swiper.css";
export default {
  name: "index",
  components: {
    swiper,
    swiperSlide,
    ServiceBar,
    Modal
  },
  data() {
    return {
      swiperOption: {
        autoplay: true,
        loop: true,
        effect: "cube",
        cubeEffect: {
          shadowOffset: 100,
          shadowScale: 0.6
        },
        pagination: {
          el: ".swiper-pagination",
          clickable: true
        },
        navigation: {
          nextEl: ".swiper-button-next",
          prevEl: ".swiper-button-prev"
        }
      },
      slideList: [
        {
          id: "42",
          img: "/imgs/slider/slide-1.jpg"
        },
        {
          id: "45",
          img: "/imgs/slider/slide-2.jpg"
        },
        {
          id: "44",
          img: "/imgs/slider/slide-3.jpg"
        },
        {
          id: "43",
          img: "/imgs/slider/slide-4.jpg"
        },
        {
          id: "41",
          img: "/imgs/slider/slide-5.jpg"
        }
      ],
      menuList: [
        [
          {
            id: 30,
            img: "/imgs/item-box-1.png",
            name: "小米CC9"
          },
          {
            id: 31,
            img: "/imgs/item-box-2.png",
            name: "小米8青春版"
          },
          {
            id: 32,
            img: "/imgs/item-box-3.jpg",
            name: "Redmi K20 Pro"
          },
          {
            id: 33,
            img: "/imgs/item-box-4.jpg",
            name: "移动4G专区"
          }
        ],
        [
          {
            id: 34,
            img: "/imgs/item-box-1.png",
            name: "小米CC9"
          },
          {
            id: 35,
            img: "/imgs/item-box-2.png",
            name: "小米8青春版"
          },
          {
            id: 36,
            img: "/imgs/item-box-3.jpg",
            name: "Redmi K20 Pro"
          },
          {
            id: 37,
            img: "/imgs/item-box-4.jpg",
            name: "移动4G专区"
          }
        ],
        [0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0],
        [0, 0, 0, 0]
      ],
      adsList: [
        {
          id: 33,
          img: "/imgs/ads/ads-1.png"
        },
        {
          id: 48,
          img: "/imgs/ads/ads-2.jpg"
        },
        {
          id: 45,
          img: "/imgs/ads/ads-3.png"
        },
        {
          id: 47,
          img: "/imgs/ads/ads-4.jpg"
        }
      ],
      phoneList: [],
      showModal: false
    };
  },
  mounted() {
    this.init();
  },
  methods: {
    // 页面加载获取数据
    init() {
      this.axios.get('/products', {
        params: {
          categoryId: 100012,
          pageSize: 14
        }
      }).then(res => {
        res.list = res.list.slice(6, 14);
        this.phoneList = [res.list.slice(0, 4), res.list.slice(4, 8)];
      })
    },
    // 添加购物车
    addCart(id) {
      this.axios.post('/carts', {
        productId: id,
        selected: true
      }).then((res) => {
        this.showModal = true;
        this.$store.dispatch('saveCartCount', res.cartTotalQuantity);
      }).catch(() => {
        this.showModal = true;
      })
    },
    // 查看购物车
    goToCart() {
      this.$router.push('/cart');
    }
  }
};
</script>

<style lang="scss">
@import "../assets/scss/config.scss";
@import "../assets/scss/mixin.scss";
.index {
  .swiper-box {
    height: 451px;
    .nav-menu {
      width: 264px;
      height: 451px;
      position: absolute;
      z-index: 9;
      background-color: rgba(85, 88, 90, 0.48);
      box-sizing: border-box;
      padding: 26px 0;
      .menu-item {
        height: 50px;
        line-height: 50px;
        &:hover {
          background-color: $colorA;
          .children {
            display: block;
          }
        }
        .item-name {
          position: relative;
          display: block;
          font-size: $fontI;
          padding-left: 30px;
          color: $colorG;
          &::after {
            content: "";
            position: absolute;
            top: 17.5px;
            right: 30px;
            @include bgImg(10px, 15px, "/imgs/icon-arrow.png");
          }
        }

        .children {
          display: none;
          position: absolute;
          left: 264px;
          width: 962px;
          top: 0;
          height: 451px;
          background-color: $colorG;
          border: 1px solid $colorH;

          ul {
            height: 75px;
            display: flex;
            li {
              height: 75px;
              line-height: 75px;
              flex: 1;
              padding-left: 23px;
              a {
                display: block;
                font-size: $fontJ;
                color: $colorB;
                padding-left: 30px;
                img {
                  width: 42px;
                  height: 35px;
                  margin-right: 15px;
                  vertical-align: middle;
                }
              }
            }
          }
        }
      }
    }

    .swiper-container {
      height: 451px;
      .swiper-button-prev {
        left: 274px;
      }
      img {
        width: 100%;
        height: 100%;
      }
    }
  }

  .ads-box {
    @include flex();
    margin-top: 14px;
    margin-bottom: 31px;
    .ads-item {
      width: 296px;
      height: 167px;
    }
  }

  .banner {
    margin-bottom: 50px;
  }

  .product-box {
    padding: 30px 0 50px;
    background-color: $colorJ;
    .pro-phone {
      font-size: 22px;
      height: 21px;
      line-height: 21px;
      color: #333;
      margin-bottom: 20px;
    }

    .wrapper {
      display: flex;
      .banner-left {
        margin-right: 16px;
        .b-img {
          width: 224px;
          height: 619px;
        }
      }

      .list {
        @include flex();
        width: 986px;
        margin-bottom: 14px;
        .item {
          width: 236px;
          height: 302px;
          background-color: $colorG;
          text-align: center;
          .product {
            display: inline-block;
            width: 67px;
            height: 24px;
            line-height: 24px;
            font-size: 14px;
            color: $colorG;
          }
          span {
            visibility: hidden;
          }
          .newProduct {
            visibility: inherit;
            background-color: #7ecf68;
          }

          .item-img {
            display: inline-block;
            width: 100%;
            height: 195px;
          }
          .item-info {
            .info-name {
              font-size: $fontJ;
              line-height: 14px;
              color: $colorB;
            }

            .info-desc {
              color: $colorD;
              line-height: 13px;
              margin: 6px auto 13px;
            }

            .info-price {
              color: #f20a0a;
              font-size: 14px;
              font-weight: 700;
              cursor: pointer;
              &:after {
                content: '';
                @include bgImg(22px, 22px, '/imgs/icon-cart-hover.png');
                vertical-align: middle;
                margin-left: 5px;
              }
            }
          }
        }
      }
    }
  }
}
</style>