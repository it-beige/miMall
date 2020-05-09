<template>
  <div class="order-pay">
    <order-header title="订单支付">
      <template v-slot:tip>
        <span>请谨防钓鱼链接或诈骗电话，了解更多></span>
      </template>
    </order-header>
    <div class="wrapper">
      <div class="container">
        <div class="order-wrap">
          <div class="item-order">
            <div class="icon-succ"></div>
            <div class="order-info">
              <h2>订单提交成功！去付款咯～</h2>
              <p>
                请在
                <span>30分</span>内完成支付, 超时后将取消订单
              </p>
              <p>收货信息：{{addressInfo}}</p>
            </div>
            <div class="order-total">
              <p>
                应付总额：
                <span>2599</span>元
              </p>
              <p>
                订单详情
                <em class="icon-down" :class="{'up': showDetail}" @click="showDetail=!showDetail"></em>
              </p>
            </div>
          </div>
          <div class="item-detail" v-if="showDetail">
            <div class="item">
              <div class="detail-title">订单号：</div>
              <div class="detail-info theme-color">{{orderId}}</div>
            </div>
            <div class="item">
              <div class="detail-title">收货信息：</div>
              <div class="detail-info">{{addressInfo}}</div>
            </div>
            <div class="item good">
              <div class="detail-title">商品名称：</div>
              <div class="detail-info">
                <ul>
                  <li v-for="(item,index) in orderDetail" :key="index">
                    <img v-lazy="item.productImage" />
                    {{item.productName}}
                  </li>
                </ul>
              </div>
            </div>
            <div class="item">
              <div class="detail-title">发票信息：</div>
              <div class="detail-info">电子发票 个人</div>
            </div>
          </div>
        </div>
        <div class="item-pay">
          <h3>选择以下支付方式付款</h3>
          <div class="pay-way">
            <p>支付平台</p>
            <div class="pay pay-ali" :class="{'checked': payType === 1}" @click="paySubmit(1)"></div>
            <div class="pay pay-wechat" :class="{'checked': payType === 2}" @click="paySubmit(2)"></div>
          </div>
        </div>
      </div>
    </div>
    <scan-pay-code v-if="showPay" @close="closePayModal" :img="payImg"></scan-pay-code>
    <modal
      title="支付确认"
      btnType="3"
      :showModal="showPayModal"
      sureText="查看订单"
      cancelText="未支付"
      @cancel="showPayModal = false"
      @submit="goOrderList"
      >
       <template v-slot:body>
        <p>您确认是否完成支付？</p>
      </template>
    </modal>
  </div>
</template>


<script>
import OrderHeader from "../components/OrderHeader";
import ScanPayCode from "../components/ScanPayCode";
import Modal from "../components/Modal";
import QRCode from 'qrcode';
export default {
  name: "order-pay",
  components: {
    OrderHeader,
    ScanPayCode,
    Modal
  },
  data() {
    return {
      orderId: this.$route.query.orderNo, // 从路由中获取参数
      addressInfo:'', // 收货人地址
      orderDetail:[], // 订单详情，包含商品列表
      payment: 0, // 订单总金额
      showDetail: false, // 是否显示订单详情
      payType: '', // 支付方式
      showPay: false, // 是否显示微信支付弹框
      payImg: '', // 微信支付的二维码地址
      showPayModal: false, // 是否显示二次支付确认弹框
      timerId: 0, // 定时器标识
      curTime: 0, // 发起支付的时间
    }
  },  
  mounted() {
    this.getOrderDetail();
  },
  methods: {
    // 获取订单详情
    getOrderDetail() {
      this.axios.get(`/orders/${this.orderId}`)
        .then(res => {
          let item = res.shippingVo;
          this.addressInfo = `${item.receiverName} ${item.receiverMobile} ${item.receiverProvince} ${item.receiverCity} ${item.receiverDistrict} ${item.receiverAddress}`;
          this.payment = res.payment;
          this.orderDetail = res.orderItemVoList;
        })
    },
    // 支付
    paySubmit(payType) {
      // 支付宝支付
      if (payType === 1) {
        this.payType = payType;
        window.open('/#/order/alipay?orderId=' + this.orderId, '_blank');
      } else {
        this.payType = payType;
        // 微信支付
        this.axios.post('/pay', {
          orderId: this.orderId,
          orderName: 'Vue高仿小米商城',
          amount: 0.01,
          payType: 2
        }).then((res) => {
          QRCode.toDataURL(res.content)
            .then(url => {
              this.payImg = url;
              this.showPay = true;
              this.curTime = Date.now();
              this.loopOrderState();
            })
            .catch(() => {
              this.$message.error('操作频繁, 请稍后重试!');
            })
        })
      }
      
    },
    // 关闭微信支付弹框
    closePayModal() {
      this.showPay = false;
      this.showPayModal = true;
      clearInterval(this.timerId);
    },
    // 轮询当前订单支付状态
    loopOrderState() {
      this.timerId = setInterval(() => {
        // 用户长时间不进行支付操作, 取消支付
        let nowTime = Date.now();
          if (nowTime - this.curTime > 7000) {
            this.$message.error('超过支付时间!');
            this.closePayModal();
            return;
          }
        this.axios.get(`/orders/${this.orderId}`)
          .then(res => {
            if (res.status == 20) {
              clearInterval(this.timerId);
              this.goOrderList();
            }
          })
      }, 2000);
    },
    // 查看订单列表
    goOrderList() {
      this.$router.push('/order/list');
    }
  }
};
</script>

<style lang="scss">
@import "../assets/scss/config.scss";
@import "../assets/scss/mixin.scss";
.order-pay {
  .wrapper {
    background-color: $colorJ;
    padding-top: 30px;
    padding-bottom: 61px;
    .order-wrap {
      padding: 62px 50px;
      background-color: $colorG;
      font-size: $fontJ;
      margin-bottom: 30px;
      .item-order {
        display: flex;
        align-items: center;
        .icon-succ {
          @include bgImg(90px, 90px, "/imgs/icon-gou.png", 60px);
          background-color: #80c58a;
          border-radius: 50%;
          margin-right: 40px;
        }
        .order-info {
          margin-right: 248px;
          h2 {
            font-size: $fontE;
            color: $colorB;
            margin-bottom: 20px;
          }
          p {
            color: $colorC;
            span {
              color: $colorA;
            }
          }
        }
        .order-total {
          & > p:first-child {
            margin-bottom: 30px;
          }
          span {
            font-size: $fontC;
            color: $colorA;
          }
          .icon-down {
            @include bgImg(14px, 10px, "/imgs/icon-down.png");
            margin-left: 9px;
            transition: all 0.5s;
            cursor: pointer;
            &.up {
              transform: rotate(180deg);
            }
          }
          .icon-up {
            transform: rotate(180deg);
          }
        }
      }
      .item-detail {
        border-top: 1px solid #d7d7d7;
        padding-top: 47px;
        padding-left: 130px;
        font-size: $fontJ;
        margin-top: 45px;
        .item {
          margin-bottom: 19px;
          .detail-title {
            float: left;
            width: 100px;
          }
          .detail-info {
            display: inline-block;
            img {
              width: 30px;
              vertical-align: middle;
            }
          }
        }
      }
    }
    .item-pay {
      padding: 26px 50px 72px;
      background-color: $colorG;
      color: $colorB;
      h3 {
        font-size: 20px;
        font-weight: 200;
        color: $colorB;
        padding-bottom: 24px;
        border-bottom: 1px solid #d7d7d7;
        margin-bottom: 26px;
      }
      .pay-way {
        font-size: 18px;
        .pay {
          display: inline-block;
          @include wh(188px, 64px);
          @include bd(1px, solid, #d7d7d7);
          cursor: pointer;
          &:last-child {
            margin-left: 20px;
          }
          &.checked {
          @include bd(1px, solid, $colorA);
          }
        }
        .pay-ali {
          background: url("/imgs/pay/icon-ali.png") no-repeat center;
          background-size: 103px 38px;
          margin-top: 19px;
        }
        .pay-wechat {
          background: url("/imgs/pay/icon-wechat.png") no-repeat center;
          background-size: 103px 38px;
        }
      }
    }
  }
}
</style>