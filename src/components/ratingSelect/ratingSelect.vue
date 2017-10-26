<template>
  <div class="ratingSelect">
    <div class="rating-type border-1px">
      <span @click="select(0, $event)" class="block positive" :class="{'active': selectType===0}">{{desc.all}}</span>
      <span @click="select(1, $event)" class="block positive" :class="{'active': selectType===1}">{{desc.positive}}</span>
      <span @click="select(2, $event)" class="block negative" :class="{'active': selectType===2}">{{desc.negative}}</span>
    </div>
    <div class="switch" :class="{'on': onlyContent}" @click="toggle">
        <span class="icon-check_circle"></span>
        <span class="text">只看有内容的评价</span>
    </div>
  </div>
</template>
<script>
  const ALL = 0
  // const positive = 1
  // const negative = 2

  export default {
    props: {
      desc: {
        type: Object,
        default () {
          return {}
        }
      },
      selectType: {
        type: Number,
        default: ALL
      },
      onlyContent: {
        type: Boolean,
        default: false
      }
    },
    methods: {
      select (type, event) {
        if (!event._constructed) {
          return
        }
        this.$emit('selectType', type)
      },
      toggle (event) {
        if (!event._constructed) {
          return
        }
        this.$emit('toggleContent', this.onlyContent)
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus">
  @import '../../common/stylus/mixin.styl'

  .ratingSelect
    .rating-type
      padding: 18px 0
      margin: 0 18px
      border-1px(rgba(7, 17, 27, 0.1))
      font-size: 0
      .block
        display: inline-block
        padding: 8px 12px
        margin-right: 8px
        line-height: 16px
        border-radius: 1px
        font-size: 12px
        color: rgb(77, 85, 93)
      .active
        color: #fff
      .positive
        background: rgba(0, 160, 220, 0.2)
        &.active
          background: rgb(0, 160, 220)
      .negative
        background: rgba(77, 85, 93, 0.2)
    .switch
      padding: 12px 18px
      font-size: 0
      border-bottom: 1px solid rgba(7, 17, 27, 0.1)
      line-height: 24px
      color: rgb(147, 153, 159)
      &.on
        .icon-check_circle
          color: #00c850
      .icon-check_circle
        display: inline-block
        vertical-align: top
        font-size: 24px
        margin-right: 4px
      .text
        display: inline-block
        vertical-align: top
        font-size: 12px
</style>