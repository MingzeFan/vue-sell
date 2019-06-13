<template>
    <div class="v-header">
        <div class="header-top">
            <div class="avatar">
            <img :src="seller.avatar" width="64px" height="64px" alt="avatar">
            </div>
            <div class="content">
                <div class="title">
                    <span class="brand"></span>
                    <span class="name">{{seller.name}}</span>
                </div>
                <div class="delivery">{{seller.description}}/{{seller.deliveryTime}}分钟送达
                </div>
                <div class="supports" v-if="seller.supports">
                    <supportIco :size="1" :type="seller.supports[0].type"></supportIco>
                    <span class="text">{{seller.supports[0].description}}</span>
                </div>
            </div>
            <div v-if="seller.supports" class="support-icon" @click="showDetail">
              <span class="support-count">{{seller.supports.length}}个</span>
              <i class="icon-keyboard_arrow_right"></i>
            </div>
        </div>
        <div class="bulletin" @click="showDetail">
            <span class="bulletin-icon"></span><span class="bulletin-text">{{seller.bulletin}}</span>
            <i class="icon-keyboard_arrow_right"></i>
        </div>
        <div class="background">
          <img :src="seller.avatar" width="100%" height="100%" alt="background">
        </div>
    </div>
</template>
<script>
import supportIco from '../support-ico/support-ico'
export default {
    props: {
        seller: {
            type: Object,
            default: {}
        }
    },
    components: {
        supportIco
    },
    methods: {
      showDetail() {
        this.headerDetailsComp = this.headerDetailsComp || this.$createHeaderDetails({
          $props: {
            seller: 'seller'
          }
        })
        this.headerDetailsComp.show()
      }
    }
}
</script>

<style lang="stylus">
@import '~common/stylus/mixin'
@import '~common/stylus/varible'
.v-header
    position relative
    color $color-white
    background $color-background-ss
    overflow hidden
    .header-top
        position relative
        display flex
        align-items center
        padding 24px 12px 18px 24px
        .avatar
            flex 0 0 64px
            width 64px
            height 64px
            margin-right 16px
            img
                border-radius 2px
        .content
            flex 1
            .title
                display flex
                align-items center
                margin-bottom 8px
                .brand
                    width: 30px
                    height: 18px
                    bg-image('brand')
                    background-size: 30px 18px
                    background-repeat: no-repeat
                .name
                    margin-left: 6px
                    font-size: 16px
                    font-weight: bold
            .delivery
                margin-bottom 10px
                font-size $fontsize-small
                line-height 12px
            .supports
                display flex
                align-items center
                .text
                    margin-left 4px
                    line-height 12px
                    font-size $fontsize-small-s
        .support-icon
          position absolute
          right 12px
          bottom 18px
          display flex
          align-items center
          padding 0 8px
          border-radius 14px
          box-sizing border-box
          height 24px
          background $color-background-sss
          .support-count
            margin-right 2px
            font-size $fontsize-small-s
          .icon-keyboard_arrow_right
            line-height 24px
            font-size $fontsize-small-s
    .bulletin
        display flex
        align-items center
        height 28px
        padding 0 12px
        background $color-background-sss
        .bulletin-icon
            flex 0 0 22px
            width 22px
            height 12px
            margin-right 4px
            background-size 22px 12px
            bg-image('bulletin')
        .bulletin-text
            flex 1
            white-space nowrap
            overflow hidden
            text-overflow ellipsis
            font-size $fontsize-small-s
        .icon-keyboard_arrow_right
            flex 0 0 10px
            width 10px
            font-size $fontsize-small-s
    .background
      position absolute
      top 0
      bottom 0
      width 100%
      z-index -1
      filter blur(10px)

</style>



