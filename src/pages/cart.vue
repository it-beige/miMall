<template>
  <div class="cart">
    <order-header title="我的购物车">
      <template v-slot:tip>
        <span>温馨提示：产品是否购买成功，以最终下单为准哦，请尽快结算</span>
      </template>
    </order-header>
    <div class="wrapper">
      <div class="container">
        <div class="cart-box">
          <ul class="cart-item-head">
            <li class="col-1">
              <span class="checkbox" :class="{'checked': selectedAll}" @click="toggleSelectAll"></span>全选
            </li>
            <li class="col-3">商品名称</li>
            <li class="col-1">单价</li>
            <li class="col-2">数量</li>
            <li class="col-1">小计</li>
            <li class="col-1">操作</li>
          </ul>
          <ul class="cart-item-list">
            <li class="cart-item" v-for="(item, index) in cartProductList" :key="index">
              <div class="item-check">
                <span class="checkbox" :class="{'checked': item.productSelected}" @click="updateCart(item)"></span>
              </div>
              <div class="item-name">
                <img v-lazy="item.productMainImage" alt />
                <span>{{item.productName + ',' + item.productSubtitle}}</span>
              </div>
              <div class="item-price">{{item.productPrice}}</div>
              <div class="item-num">
                <div class="num-box">
                  <a href="javascript:;" @click="updateCart(item, '-')">-</a>
                  <span>{{item.quantity}}</span>
                  <a href="javascript:;" @click="updateCart(item, '+')">+</a>
                </div>
              </div>
              <div class="item-total">{{item.productTotalPrice}}</div>
              <div class="item-del" @click="showHintModal(item)"></div>
            </li>
          </ul>
        </div>
        <div class="order-wrap clearfix">
          <div class="cart-tip fl">
            <a href="/">继续购物</a>
            共
            <span>{{cartProductList.length}}</span>件商品，已选择
            <span>{{checkedNum}}</span>件
          </div>
          <div class="total fr">
            合计：
            <span>{{cartTotalPrice}}</span>元
            <a href="javascript:;" class="btn" @click="order">去结算</a>
          </div>
        </div>
      </div>
    </div>
    <service-bar></service-bar>
    <nav-footer></nav-footer>
    <modal 
    title="提示" 
    sureText="确定"
    cancelText="取消"
    btnType='3'
    modalType="middle"
    :showModal="showModal"
    @submit="deleteProduct"
    @cancel="showModal = false"
    >
    <template v-slot:body>
      <p>你确定要删除此商品吗?</p>
    </template>
    </modal>
  </div>
</template>


<script>
import OrderHeader from "../components/OrderHeader";
import ServiceBar from "../components/ServiceBar";
import NavFooter from "../components/NavFooter";
import Modal from "../components/Modal";
export default {
  name: "cart",
  components: {
    OrderHeader,
    NavFooter,
    ServiceBar,
    Modal
  },
  data() {
    return {
      productId: 0, // 商品id
      showModal: false, // 控制模态框显示和隐藏
      cartProductList: [], // 购物车商品列表
      selectedAll: false, // 商品是否全选中
      cartTotalPrice: 0, // 商品总金额
      checkedNum: 0, // 选中商品总数
      cartTotalQuantity: 0, // 商品总数
    }
  },
  mounted() {
    // 获取购物车列表
    this.getCartList();
  },
  methods: {
    // 获取购物车列表
    getCartList() {
      this.axios.get('/carts')
        .then(res => {
          this.renderData(res);
      })
    },
    // 获取数据
    renderData(res) {
      this.productId = res.productId;
      this.cartProductList = res.cartProductVoList || [];
      this.selectedAll = res.selectedAll;
      this.cartTotalPrice = res.cartTotalPrice;
      this.checkedNum = res.cartProductVoList.filter(item => item.productSelected).length;
    },
    // 全选切换状态
    toggleSelectAll() {
      let url = this.selectedAll ? '/carts/unSelectAll' : '/carts/selectAll';
      this.axios.put(url).then((res) => {
        this.renderData(res);
      })
    },
    // 更新购物车数量和购物车单选状态
    /**
     * @param {object} item: 每一项的内容
     * @param {string} type: 控制商品加减
     */
    updateCart(item, type) {
      // quantity 商品数量
      // selected 商品是否选中
      // productStock 商品库存
      let quantity = item.quantity,
          selected = item.productSelected,
          productStock = item.productStock;
      if (type === '-') {
        if (quantity === 1) {
          this.$message.warning('商品至少保留一件');
          return;
        }
        --quantity;
      } else if (type === '+') {
        if (quantity > productStock) {
          this.$message.warning('购买数量不能超过库存数量');
          return;
        }
        ++quantity;
      } else {
        selected = !selected;
      }

      this.axios.put(`/carts/${item.productId}`, {
        quantity,
        selected
      })
        .then(res => {
          this.renderData(res);
        })
    },
    // 删除商品提示框
    showHintModal(item) {
      this.showModal = true;
      this.productId = item.productId;
    },
    // 删除购物车商品
    deleteProduct() {
      this.axios.delete(`/carts/${this.productId}`)
        .then(res => {
          this.showModal = false;
          this.renderData(res);
        })
    },
    // 购物车下单
    order() {
      let flag = this.cartProductList.some(item => item.productSelected);
      if (!flag) {
        this.$message.warning('请选择一件商品进行支付!');
        return;
      }
      this.$router.push('/order/confirm');
    }
  }

};
</script>

<style lang="scss">
@import "../assets/scss/config.scss";
@import "../assets/scss/mixin.scss";
.cart {
  .wrapper {
    background-color: $colorJ;
    padding-top: 33px;
    padding-bottom: 114px;
    .cart-box {
      background-color: $colorG;
      font-size: $fontJ;
      color: $colorD;
      text-align: center;
      .checkbox {
        display: inline-block;
        @include wh(22px, 22px);
        @include bd();
        vertical-align: middle;
        margin-right: 17px;
        cursor: pointer;
        &.checked {
          background: url("/imgs/icon-gou.png") $colorA no-repeat center;
          background-size: 16px 12px;
          border: none;
        }
      }
      .cart-item-head {
        display: flex;
        @include hl(79px, 79px);
        .col-1 {
          flex: 1;
        }
        .col-2 {
          flex: 2;
        }
        .col-3 {
          flex: 3;
        }
      }
      .cart-item-list {
        .cart-item {
          display: flex;
          align-items: center;
          height: 125px;
          border-top: 1px solid #e5e5e5;
          font-size: $fontI;
          .item-check {
            flex: 1;
          }
          .item-name {
            flex: 3;
            font-size: $fontH;
            color: $colorB;
            display: flex;
            align-items: center;
            img {
              @include wh(80px, 80px);
              vertical-align: middle;
            }
            span {
              margin-left: 30px;
            }
          }
          .item-price {
            flex: 1;
            color: $colorB;
          }
          .item-num {
            flex: 2;
            .num-box {
              display: inline-block;
              @include wh(150px, 40px);
              @include bd();
              line-height: 40px;
              font-size: $fontJ;
              a {
                display: inline-block;
                width: 50px;
                color: $colorB;
              }
              span {
                display: inline-block;
                width: 50px;
                color: $colorB;
              }
            }
          }
          .item-total {
            flex: 1;
            color: $colorA;
          }
          .item-del {
            flex: 1;
            @include bgImg(14px, 12px, "/imgs/icon-close.png");
            cursor: pointer;
          }
        }
      }
    }

    .order-wrap {
      @include hl(50px, 50px);
      font-size: $fontJ;
      color: $colorC;
      margin-top: 20px;
      
      .cart-tip {
        margin-left: 29px;
        a {
          color: $colorC;
          margin-right: 37px;
        }
        span {
          color: $colorA;
          margin: 0 5px;
        }
      }
      .total {
        font-size: $fontJ;
        color: $colorA;
        span {
          font-size: 24px;
        }
        a {
          @include wh(202px, 50px);
          line-height: 50px;
          font-size: $fontH;
          margin-left: 37px;
        }
      }
    }
  }
}
</style>