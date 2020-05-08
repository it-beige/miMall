<template>
  <div class="order-list">
    <order-header title="订单列表">
      <template v-slot:tip>
        <span>请谨防钓鱼链接或诈骗电话，了解更多></span>
      </template>
    </order-header>
    <div class="wrapper">
      <div class="container">
        <div class="order-box">
          <loading v-if="loading"></loading>
          <div class="order" v-for="(item, i) in orderList" :key="i">
            <div class="order-title">
              <div class="item-info fl">
                {{item.createTime}}
                <span>|</span>
                {{item.receiverName}}
                <span>|</span>
                订单号：{{item.orderNo}}
                <span>|</span>
                {{item.paymentTypeDesc}}
              </div>
              <div class="item-money fr">
                <span>应付金额：</span>
                <span class="money">{{item.payment}}</span>
                <span>元</span>
              </div>
            </div>
            <div class="order-content clearfix" v-for="(order, i) in item.orderItemVoList" :key='i'>
              <div class="good-box fl">
                <div class="good-list">
                  <div class="good-img">
                    <img v-lazy="order.productImage" alt="">
                  </div>
                  <div class="good-name">
                    <div class="p-name">{{order.productName}}</div>
                    <div class="p-money">{{order.currentUnitPrice}} X {{order.quantity}}</div>
                  </div>
                </div>
              </div>
              <div class="good-state fr">
                <a href="javascript:;" @click="gotoPay(order.orderNo)">{{item.statusDesc}}</a>
              </div>
            </div>
          </div>
          <el-pagination
            class="pagination"
            background
            layout="prev, pager, next"
            :pageSize="pageSize"
            :total="total"
            @current-change="handleChange"
            >
          </el-pagination>
          <no-data v-if="!loading && orderList.length == 0"></no-data>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import OrderHeader from "../components/OrderHeader";
import Loading from "../components/Loading";
import NoData from "../components/NoData";
import { Pagination } from 'element-ui';
export default {
  name: "order-list",
  components: {
    OrderHeader,
    Loading,
    NoData,
    [Pagination.name]: Pagination,
  },
  data() {
    return {
      loading: true,
      orderList: [], // 订单信息
      pageSize: 10,
      pageNum: 1,
      total: 0,
    }
  },
  mounted() {
    this.getOrderList();
  },
  methods: {
    // 获取所有订单信息
    getOrderList() {
      this.axios.get('/orders', {
        params: {
          pageSize:10,
          pageNum:this.pageNum
        }
      })
        .then(res => {
          this.loading = false;
          this.orderList = res.list;
          this.total = res.total;
        }).catch(() => {
          this.loading = false;
        })
    },
    // 支付订单
    gotoPay(orderNo) {
      this.$router.push({
        path: '/order/pay',
        query: {
          orderNo
        }
      })
    },
    // 第一种方法：分页器
    handleChange(pageNum){
      this.pageNum = pageNum;
      this.getOrderList();
    },
  }
};
</script>

<style lang="scss">
@import "./../assets/scss/config.scss";
@import "./../assets/scss/mixin.scss";
.order-list {
  .wrapper {
    background-color: $colorJ;
    padding-top: 33px;
    padding-bottom: 110px;
    .order-box {
      .order {
        @include bd();
        background-color: $colorG;
        margin-bottom: 31px;
        &:last-child {
          margin-bottom: 0;
        }
        .order-title {
          @include hl(74px, 74px);
          background-color: $colorK;
          padding: 0 43px;
          font-size: 16px;
          color: $colorC;
          .item-info {
            span {
              margin: 0 9px;
            }
          }
          .money {
            font-size: 26px;
            color: $colorB;
          }
        }
        .order-content {
          padding: 0 43px;
          .good-box {
            width: 88%;
            .good-list {
              display: flex;
              align-items: center;
              height: 145px;
              .good-img {
                width: 112px;
                img {
                  width: 100%;
                }
              }
              .good-name {
                font-size: 20px;
                color: $colorB;
              }
            }
          }
          .good-state {
            @include hl(145px, 145px);
            font-size: 20px;
            color: $colorA;
            a {
              color: $colorA;
            }
          }
        }
      }
      .pagination {
        text-align: right;
      }
      .el-pagination.is-background .el-pager li:not(.disabled).active {
        background-color: $colorA;
      }
      .el-button--primary {
        background-color: $colorA;
        border-color: $colorA;
      }
    }
  }
}
</style>