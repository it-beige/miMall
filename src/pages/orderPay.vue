<template>
  <div class="order-pay">
   <order-header title="订单支付">
      <template v-slot:tip>
        <span>请谨防钓鱼链接或诈骗电话，了解更多></span>
      </template>
    </order-header>
  </div>
</template>


<script>
import OrderHeader from "../components/OrderHeader";
export default {
  name: 'order-pay',
  components: {
    OrderHeader
  }
}
</script>

<style scoped>

</style>