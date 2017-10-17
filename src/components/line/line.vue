<template>
  <div class="line">
	<div class="line-wrapper">
	  <div class="line-it"></div>
	  <div class="text">{{text}}</div>
	  <div class="line-it"></div>
	</div>
  </div>
</template>
<script>
  export default {
    props: {
      text: {
        type: String
      }
    }
  }
</script> 
<style lang="stylus" rel="stylesheet/stylus">
  .line
    .line-wrapper
      display: flex
      .line-it
      	flex: 1
      	position: relative
      	top: -6px
      	border-bottom: 1px solid rgba(255, 255, 255, 0.2)
      .text
      	padding: 0 12px
      	font-weight: 700
      	font-size: 14px
</style>