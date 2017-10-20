<template>
  <div class="goods">
  	<div class="menu-wrapper" ref="menuWrapper">
  	  <ul>
  	  	<li v-for="(item, index) in goods" class="menu-item" :class="{current:currentIndex==index}" @click="selectMenu(index, $event)">
  	  	  <span class="text border-1px">
  	  	  	<span v-show="item.type > 0" class="icon" :class="classMap[item.type]"></span>{{ item.name }}
  	  	  </span>
  	  	</li>
  	  </ul>
  	</div>
  	<div class="goods-wrapper" ref="goodsWrapper">
      <ul>
        <li v-for="item in goods" class="food-list food-list-hook">
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li v-for="food in item.foods" class="food-item">
              <div class="icon">
                <img :src="food.icon" width="57" height="57">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}</span><span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">&yen;{{food.price}}</span><span class="old" v-show="food.oldPrice">{{food.oldPrice}}</span>
                </div>
                <div class="cartcontrol-wrapper">
                  <v-cartcontrol :food="food"></v-cartcontrol>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul> 
    </div>
    <v-shopCart :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></v-shopCart>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'

  import shopCart from '../shopCart/shopCart.vue'
  import cartcontrol from '../cartcontrol/cartcontrol.vue'

  export default {
    data () {
      return {
        goods: {},
        listHeight: [],
        scrollY: 0
      }
    },
    props: {
      seller: {
        type: Object
      }
    },
    created () {
      this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee']

      this.$http.get('/api/goods').then((response) => {
        if (response.data.errno === 0) {
          this.goods = Object.assign({}, this.goods, response.data.data)
          this.$nextTick(() => {
            this._initScroll()
            this._calculateHeight()
          })
        }
      })
    },
    computed: {
      currentIndex () {
        for (let i = 0; i < this.listHeight.length; i++) {
          let height1 = this.listHeight[i]
          let height2 = this.listHeight[i + 1]
          if (!height2 || (this.scrollY >= height1 && this.scrollY < height2)) {
            return i
          }
        }
        return 0
      }
    },
    methods: {
      _initScroll () {
        this.menuScroll = new BScroll(this.$refs.menuWrapper, {
          click: true
        })
        this.goodsScroll = new BScroll(this.$refs.goodsWrapper, {
          click: true,
          probeType: 3
        })
        this.goodsScroll.on('scroll', (pos) => {
          this.scrollY = Math.abs(Math.round(pos.y))
        })
      },
      _calculateHeight () {
        let foodList = this.$refs.goodsWrapper.getElementsByClassName('food-list-hook')
        let height = 0
        this.listHeight.push(height)
        for (let i = 0; i < foodList.length; i++) {
          let item = foodList[i]
          height += item.clientHeight
          this.listHeight.push(height)
        }
      },
      selectMenu (index, event) {
        if (!event._constructed) {
          return
        }
        let foodList = this.$refs.goodsWrapper.getElementsByClassName('food-list-hook')
        let el = foodList[index]
        this.goodsScroll.scrollToElement(el, 300)
      }
    },
    components: {
      'v-shopCart': shopCart,
      'v-cartcontrol': cartcontrol
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin"; 

  .goods
    display: flex
    position: absolute
    top: 174px
    bottom: 46px
    width: 100%
    overflow: hidden
    .menu-wrapper
      flex: 0 0 80px
      width: 80px
      background: #f3f5f7
      .menu-item
        display: table
        height: 54px
        width: 56px
        padding: 0 12px
        line-height: 14px
        &.current
          position: relative
          z-index: 10
          margin-top: -1px
          background: #fff 
          .text
            font-weight: 700
            border-none()
      .icon
        display: inline-block
        vertical-align: top
        width: 12px
        height: 12px
        margin-right: 2px
        background-size: 12px
        background-repeat: no-repeat
        &.decrease
          bg-image('decrease_3')
        &.discount
          bg-image('discount_3')
        &.guarantee
          bg-image('guarantee_3')
        &.invoice
          bg-image('invoice_3')
        &.special
          bg-image('special_3') 
      .text
        display: table-cell
        width: 56px
        vertical-align: middle
        border-1px(rgba(7, 17, 27, 0.1))
        font-size: 12px
    .goods-wrapper
      flex: 1
      .title
        padding-left: 18px
        line-height: 26px
        font-size: 12px
        color: rgb(147, 153, 159)
        background: #f3f5f7
        border-left: 2px solid #d9dde1
      .food-item
        position: relative
        display: flex
        margin: 18px
        padding-bottom: 18px
        border-bottom: 1px solid rgba(7, 17, 27, 0.1)
        &:last-child
          border: none
        .icon
          flex: 0 0 57px
          margin-right: 10px
        .content
          flex: 1
          .name
            line-height: 14px
            font-size: 14px
            color: rgb(7, 17, 27)
            margin: 2px 0 8px
          .desc, .extra
            margin-bottom: 8px
            line-height: 14px
            font-size: 10px
            color: rgb(147, 153, 159)
          .extra
            .count
              margin-right: 8px
          .price
            font-weight: 700
            line-height: 24px
            .now
              margin-right: 8px
              font-size: 14px
              color: rgb(240, 20, 20)
            .old
              text-decoration: line-through
              font-size: 10px
              color: rgb(147, 153, 159)
          .cartcontrol-wrapper
            position: absolute
            right: 0
            bottom: 12px                        
</style>