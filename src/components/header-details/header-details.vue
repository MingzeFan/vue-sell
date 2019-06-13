<template>
<transition name="fade">
    <div class="header-details" v-show="visible">
        <div class="detail-wrapper">
            <div class="detail-main">
                <h1 class="name">{{seller.name}}</h1>
                <div class="star-wrapper">
                    <star :size="48" :score="seller.score"></star>
                </div>
                <div class="title">
                    <div class="line"></div>
                    <div class="text">优惠信息</div>
                    <div class="line"></div>
                </div>
                    <ul class="supports">
                        <li class="support-item" v-for="(support, index) in seller.supports" :key="index">
                            <supportIco :size="2" :type="support.type"></supportIco>
                            <span class="text">{{support.description}}</span>
                        </li>
                    </ul>
                <div class="title">
                    <div class="line"></div>
                    <div class="text">商家公告</div>
                    <div class="line"></div>
                </div>
                <div class="bulletin">
                    <p class="content">{{seller.bulletin}}</p>
                </div>
            </div>
        </div>
        <div class="detail-close">
            <i class="icon-close" @click="hide"></i>
        </div>
    </div>
</transition>
</template>

<script>
import star from 'components/star/star'
import supportIco from 'components/support-ico/support-ico'
export default {
    name: 'header-details',
    data() {
        return {
            visible: false
        }
    },
    props: {
        seller: {
            type: Object,
            default: {}
        }
    },
    components: {
        star,
        supportIco
    },
    methods: {
        show() {
            this.visible = true
        },
        hide() {
            this.visible = false
        }
    }
    
}
</script>

<style lang="stylus">
@import '~common/stylus/mixin'
@import '~common/stylus/varible'
.header-details
    position fixed
    top 0
    left 0
    z-index 100
    width 100%
    height 100%
    overflow auto
    background $color-background-s
    color $color-white
    opacity 1
    backdrop-filter blur(10px)
    &.fade-enter-active, &.fade-leave-active
        transition all 0.5s
    &.fade-enter, &.fade-leave-to
        opacity 0
        background $color-background
    .detail-wrapper
        min-height 100%
        display inline-block
        .detail-main
            margin-top 64px
            padding 0 36px 64px 36px
            .name
                margin-bottom 16px
                line-height: 16px
                font-size: $fontsize-large
                font-weight: 700
                text-align center
            .star-wrapper
                margin-bottom 28px
            .title
                display flex
                margin-bottom 24px
                .line
                    flex 1
                    position relative
                    top -6px
                    border-bottom 1px solid rgba(255, 255, 255, 0.2) 
                .text
                    padding 0 12px
                    font-weight: 700
                    line-height 14px
                    font-size: $fontsize-medium
            .supports
                padding 0 12px 28px 12px
                .support-item
                    display flex
                    align-items center
                    margin-bottom 12px
                    .text
                        margin-left 6px
                        font-size: $fontsize-small
            .bulletin
                padding 0 12px
                .content
                    line-height: 24px
                    font-size: $fontsize-small
    .detail-close
        margin-top -64px
        clear both
        text-align center
        .icon-close
            font-size $fontsize-large-xxxx
</style>


