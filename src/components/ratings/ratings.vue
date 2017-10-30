<template>	
	<div class="ratings" ref="ratings">
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
    <div class="ratingWrapper">
      <ul>
        <li class="rating-lsit border-1px" v-for="rating in ratings">
          <div class="avatar">
            <img :src="rating.avatar" width="28" height="28">
          </div>
          <div class="content">
            <h2 class="name">{{rating.username}}</h2>
            <div class="star-wrapper">
              <v-star :score="4" :size="24"></v-star>
              <span class="delivery" v-show="rating.delivery">{{rating.deliveryTime}}分钟送达</span>
            </div>
            <p class="text">{{rating.text}}</p>
            <div class="recommend">
              <span class="icon-thumb_up"></span>
              <span v-for="item in rating.recommend" class="item">{{item}}</span>
            </div>
            <div class="time">2017-10-30 23:26</div>
          </div>
        </li>
      </ul>
    </div>   
    </div>
	</div>
</template>
<script>
  import star from '../star/star.vue'
  import split from '../split/split.vue'
  import ratingSelect from '../ratingSelect/ratingSelect.vue'

  import BScroll from 'better-scroll'

  const ALL = 2

  export default {
    props: {
      seller: {
        type: Object
      }
    },
    data () {
      return {
        ratings: [],
        desc: {
          all: '全部',
          positive: '满意',
          negative: '不满意'
        },
        selectType: ALL
      }
    },
    created () {
      this.$http.get('api/ratings').then((response) => {
        if (response.data.errno === 0) {
          this.ratings = response.data.data
          this.$nextTick(() => {
            this.scroll = new BScroll(this.$refs.ratings, {
              click: true
            })
          })
        }
      })
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
  @import "../../common/stylus/mixin.styl"
  
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
    .ratingWrapper
      padding: 0 18px
      .rating-lsit
        display: flex
        padding: 18px 0
        border-1px(rgba(7, 17, 27, 0.1))
        font-size: 0
        .avatar
          flex: 0 0 28px
          margin-right: 12px
          width: 28px
          img
            border-radius: 50%
        .content
          flex: 1
          .name
            line-height: 12px
            margin-bottom: 4px
            font-size: 10px
            color: rgb(7, 17, 27)
          .star-wrapper
            margin-bottom: 6px
            font-size: 0
            .star
              display: inline-block
              vertical-align: top
              margin-right: 6px
            .delivery
              display: inline-block
              vertical-align: top
              line-height: 12px
              font-size: 10px
              font-weight: 200
              color: rgb(147, 153, 159)
          .text
            line-height: 18px
            margin-bottom: 8px
            font-size: 12px
            color: rgb(7, 17, 27)
          .recommend
            font-size: 0
            .icon-thumb_up
              display: inline-block
              line-height: 16px
              margin: 0 8px 4px 0
              font-size: 12px
              color: rgb(0, 160, 220)
            .item
              display: inline-block
              padding: 4px 6px
              margin-right: 8px
              border: 1px solid rgba(7, 17, 27, 0.1)
              background: rgb(277, 255, 255)
              border-radius: 2px
              font-size: 9px
              color: rgb(147, 153, 159)
              &:last-child
                margin: 0
            
          
</style>