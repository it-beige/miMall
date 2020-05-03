<template>
  <div class="service">
    <div class="container">
      <ul>
        <li><span class="icon inco-setting"></span>预约维修服务</li>
        <li><span class="icon icon-7day"></span>7天无理由退货</li>
        <li><span class="icon icon-15day"></span>15天免费换货</li>
        <li><span class="icon icon-post"></span>满150元包邮</li>
      </ul>
    </div>
  </div>
</template>


<script>
export default {
  name: 'service-bar'
}
</script>

<style lang="scss">
@import '../assets/scss/config.scss';
@import '../assets/scss/mixin.scss';
.service {
  font-size: $fontI;
  color: $colorC;
  padding: 33px 0;
  li {
    display: inline-block;
    width: 24.9%;
    text-align: center;
    
  }
  .icon {
    @include bgImg(22px, 22px, '/imgs/icon-setting.png');
    vertical-align: middle;
    margin-right: 8px;
  }
  .icon-7day {
    background: url('/imgs/icon-7day.png') no-repeat center;
    background-size: contain;
  }
  .icon-15day {
    background: url('/imgs/icon-15day.png') no-repeat center;
    background-size: contain;
  }
  .icon-post {
    background: url('/imgs/icon-post.png') no-repeat center;
    background-size: contain;
  }
}
</style>