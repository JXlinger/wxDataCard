<template>
    <view class="start" :style="{ height: wHeight + 'px' }">
        <view :animation="onAnimation" class="on_animation">
            <view class="Qr_code">
                <image src="../../static/image/Qr_code.png" mode="widthFix"></image>
            </view>
        </view>
        <view :animation="underAnimation" class="under_animation">
            <image class="wave" src="../../static/image/wave.png" mode="aspectFill"></image>
            <image class="wave wave-bg" src="../../static/image/wave.png" mode="aspectFill"></image>
            <button type="primary" @tap="toIndex">去首页</button>
        </view>
        
    </view>
</template>

<script>
const app = getApp();
export default {
    data() {
        return {
            wHeight: null,
            wWidth: null,
            onAnimation: {},
            underAnimation: {}
        };
    },
    onLoad() {
        console.log(app.globalData);
        let that = this;
        uni.getSystemInfo({
            success(res) {
                app.globalData.systemInfo = res;
                that.wHeight = res.windowHeight;
                that.wWidth = res.windowWidth;
            }
        });
    },
    onShow() {
        var animation= uni.createAnimation({
            duration: 600,
            timingFunction: 'ease-out'
        });
        var unanimation = uni.createAnimation({
            duration: 1500,
            timingFunction: 'ease-in-out'
        });
        
        this.animation = animation;
        this.unanimation = animation;
        
        setTimeout(function() {
                animation.width(this.wWidth).backgroundColor('#26daf7').step();
                this.onAnimation = animation.export();
        }.bind(this),100);
        setTimeout(function() {
                unanimation.height(this.wHeight - uni.upx2px(530)).step();
                this.underAnimation = unanimation.export();
        }.bind(this),900);
    },
    methods: {
        toIndex(){
            uni.switchTab({
                url: '../index/index'
            })
        }
    }
};
</script>

<style lang="less">
.start {
    width: 100%;
    position: relative;
}
.on_animation {
    width: 0%;
    // background: #26daf7;
    height: 100%;
    overflow: hidden;
    .Qr_code{
        width: 350upx;
        margin: 0 auto;
        padding-top: 80upx;
        image{
            width: 100%;
        }
    }
}
.under_animation {
    width: 100%;
    height: 0%;
    background: #D2EFF4;
    position: absolute;
    bottom: -260rpx;
    button{
        display: table;
        width: 300rpx;
        font-size: 28rpx;
        text-align: center;
    }
}
.wave {
  position: absolute;
  z-index: 3;
  right: 0;
  top: -260rpx;
  opacity: .6;
  height: 260rpx;
  width: 2250rpx;
  animation: wave 10s linear infinite;
}
.wave-bg {
  z-index: 1;
  animation: wave-bg 10s linear infinite;
}
@keyframes wave{
  from {transform: translate3d(125rpx,0,0);}
  to {transform: translate3d(1125rpx,0,0);}
}
@keyframes wave-bg{
  from {transform: translate3d(375rpx,0,0);}
  to {transform: translate3d(1375rpx,0,0);}
}
</style>
