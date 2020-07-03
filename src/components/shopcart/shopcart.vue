<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo" :class="{'highlight': totalCount > 0}">
                        <i class="icon-shopping_cart" :class="{'highlight': totalCount > 0}"></i>
                    </div>
                    <div class="num" v-show="totalCount > 0">
                        {{totalCount}}
                    </div>
                </div>
                <div class="price" :class="{'highlight': totalPrice > 0}">{{totalPrice}}元</div>
                <div class="desc">另需配送费￥{{deliveryprice}}元</div>

            </div>
            <div class="content-right" >
                <div class="pay" :class="payClass">
                    {{payDesc}}
                </div>
            </div>
        </div>
        <!-- <div class="ball-container" >
          <div transition="drop" v-for="(ball, index) in balls" v-show="ball.show" class="ball" :key="index">
            <div class="inner"></div>
          </div>
        </div> -->
    </div>
</template>

<script>
export default {
  name: 'Shopcart',
  props: {
    selectFoods: {
      type: Array,
      default () {
        return []
      }
    },
    deliveryprice: {
      type: Number,
      default: 0
    },
    minprice: {
      type: Number,
      default: 0
    }
  },

  data () {
    return {
      // balls: [{
      //   show: false
      // }]
    }
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFoods.forEach((food) => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let count = 0
      this.selectFoods.forEach((food) => {
        count += food.count
      })
      return count
    },
    payDesc () {
      if (this.totlaPrice === 0) {
        return `￥${this.minprice}元起送`
      } else if (this.totalPrice < this.minprice) {
        let diff = this.minprice - this.totalPrice
        return `还差￥${diff}元起送`
      } else {
        return '去结算'
      }
    },
    payClass () {
      if (this.totalPrice < this.minprice) {
        return 'not-enough'
      } else {
        return 'enough'
      }
    }
  }
}

</script>

<style lang="stylus">
.shopcart
    position: fixed
    left:0
    bottom: 0
    z-index:50
    width:100%
    height:48px
    .content
        display: flex
        background: #141d27
        font-size: 0 //消除inline-block的间隔
        .content-left
            flex: 1
            .logo-wrapper
                display:inline-block
                position: relative
                top: -10px
                margin: 0 12px
                padding: 6px
                width: 56px
                height: 56px
                box-sizing: border-box
                vertical-align :top
                border-radius: 50%
                background: #141d27
                .logo
                    width:100%
                    height:100%
                    border-radius: 50%
                    background: #2b343c
                    text-align: center
                    &.highlight
                        background: rgb(0,160,220)
                    .icon-shopping_cart
                        line-height: 44px
                        font-size:24px
                        color: #80858a
                        &.highlight
                            color: #fff
                .num
                    position: absolute
                    top:0
                    right:0
                    width: 24px
                    height: 16px
                    line-height:16px
                    text-align: center
                    border-radius: 16px
                    font-size: 9px
                    font-weight : 700
                    color: #ffffff
                    background: rgb(240,20,20)
                    box-shadow: 0 4px 8px 0 rgba(0,0,0,.4)
            .price
                display:inline-block
                vertical-align :top
                margin-top: 12px
                line-height: 24px
                box-sizing: border-box
                padding-right: 12px
                border-right : 1px solid rgba(255,255,255,0.1)
                font-size: 16px
                font-weight: 700
                color: rgba(255,255,255,0.4)
                &.highlight
                    color: #fff
            .desc
                display:inline-block
                vertical-align: top
                margin: 12px 0 0 12px
                line-height: 24px
                color: rgba(255,255,255,0.4)
                font-size: 10px
        .content-right
            flex: 0 0 105px
            width: 105px
            .pay
                height: 48px
                line-height: 48px
                text-align: center
                font-size: 12px
                font-weight: 700
                color: rgba(255,255,255,0.4)
                &.not-enough
                    background: #2b333b
                &.enough
                    background: #00b43c
                    color: #fff
</style>
