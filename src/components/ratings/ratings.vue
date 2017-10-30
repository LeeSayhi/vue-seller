<template>	
	<div class="ratings">
		<div class="rating-contente">
    <div class="overview">
      <div class="overview-left">
        <h1 class="score">3.9</h1>
        <div class="title">综合评分</div>
        <div class="rank">高于周边商家62.8%</div>
      </div>
      <div class="overview-right">
        <div class="score-wrapper">
          <span class="title">服务态度</span>
          <v-star :size="36" :score="3.9"></v-star>
          <span class="score">3.9</span>
        </div>
        <div class="score-wrapper">
          <span class="title">商品评分</span>
          <v-star :size="36" :score="4"></v-star>
          <span class="score">4.0</span>
        </div>
        <div class="delivery-wrapper">
          <span class="title">送达时间</span>
          <span class="delivery">10分钟</span>
        </div>
      </div>
    </div>
    <v-split></v-split>
    <v-ratingSelect :desc="desc" :select-type="selectType" @selectType="ratingType"></v-ratingSelect>
    <div class="ratingWrapper"></div>   
    </div>
	</div>
</template>
<script>
  import star from '../star/star.vue'
  import split from '../split/split.vue'
  import ratingSelect from '../ratingSelect/ratingSelect.vue'

  const ALL = 2

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        desc: {
          all: '全部',
          positive: '满意',
          negative: '不满意'
        },
        selectType: ALL
      }
    },
    methods: {
      ratingType (type) {
        this.selectType = type
      }
    },
    components: {
      'v-star': star,
      'v-split': split,
      'v-ratingSelect': ratingSelect
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
  .ratings
    position: absolute
    top: 174px
    left: 0
    bottom: 0
    width: 100%
    overflow: hidden
    .overview
      display: flex
      padding: 18px 0
      .overview-left
        flex: 0 0 137
        width: 137px
        padding: 6px 0
        text-align: center
        @media only screen and (max-width)
          flex: 0 0 120px
          width: 120px
        .score
          line-height: 28px
          margin-bottom: 6px
          font-size: 24px
          color: rgb(288, 153, 0)
        .title
          margin-bottom: 8px
          line-height: 12px
          font-size: 12px
          color: rgb(7, 17, 27)
        .rank
          line-height: 10px
          font-size: 10px
          color: rgb(147, 153, 159)
      .overview-right
        flex: 1
        padding: 6px 0 6px 24px
        @media only screen and (max-width)
          margin-left: 6px
        .score-wrapper
          margin-bottom: 6px
          font-size: 0
          .title
            display: inline-block
            vertical-align: top
            line-height: 18px
            font-size: 12px
            color: rgb(7, 17, 27)
          .star
            display: inline-block
            vertical-align: top
            margin: 0 12px
          .score
            display: inline-block
            line-height: 18px
            font-size: 12px
            color: rgb(255, 153, 0)
        .delivery-wrapper
          font-size: 0
          .title
            line-height: 18px
            font-size: 12px
            color: rgb(7, 17, 27)
          .delivery
            margin-left: 12px
            font-size: 12px
            color: rgb(147, 153, 159)
        
</style>