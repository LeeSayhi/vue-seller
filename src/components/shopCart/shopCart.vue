<template>
  <div class="shopCart-wrapper">
    <div class="shopCart">
      <div class="content">
      	<div class="content-left">
      	  <div class="logo-wrapper">
      	  	<div class="logo">
      	  	  <i class="icon-shopping_cart"></i>
      	  	</div>
      	  	<div class="num"></div>
      	  </div>
      	  <div class="price">&yen;0</div>
      	  <div class="desc">另虚配送费&yen;{{deliveryPrice}}元</div>
      	</div>
      	<div class="content-right"></div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    props: {
      deliveryPrice: {
        type: Number,
        default: 0
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
  .shopCart-wrapper
    position: fixed
    left: 0
    bottom: 0
    z-index: 50
    width: 100%
    height: 48px
    .content
      display: flex
      background: #141d27
      font-size: 0
      color: rgba(255, 255, 255, 0.4)
      .content-left
        flex: 1
        .logo-wrapper
          display: inline-block
          vertical-align: top
          position: relative
          top: -10px
          margin: 0 12px
          padding: 6px
          width: 56px
          height: 56px
          box-sizing: border-box
          border-radius: 50%
          background: #141d27
          .logo
          	width: 100%
          	height: 100%
          	border-radius: 50%
          	text-align: center
          	background: #2b343c
          	.icon-shopping_cart
          	  line-height: 44px
          	  font-size: 24px
          	  color: #80858a
        .price
          display: inline-block
          vertical-align: top
          margin-top: 12px
          line-height: 24px
          padding-right: 12px
          box-sizing: border-box
          border-right: 1px solid rgba(255, 255, 255, 0.1)
          font-size: 16px
          font-weight: 700
        .desc
          display: inline-block
          vertical-align: top
      .content-right
      	flex: 0 0 105px	
</style>