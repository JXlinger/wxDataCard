<template>
    <view class="about">
        <view class="top_img"><image :src="userInfo.avatarUrl" mode="widthFix"></image></view>
        <view class="user">
            <image :src="userInfo.avatarUrl" mode="widthFix"></image>
            <view class="name">{{ userInfo.nickName }}</view>
            <view class="setting" @tap="openSetting"></view>
        </view>
    </view>
</template>

<script>
const app = getApp();
export default {
    data() {
        return {
            userInfo: {}
        };
    },
    onLoad() {
        const that = this;
        if (app.globalData.UserInfo) {
            this.userInfo = app.globalData.UserInfo;
        } else {
            uni.getUserInfo({
                success(res) {
                    that.userInfo = res.userInfo
                }
            })
        }
    },
    methods: {
        openSetting(){
            uni.getSetting({
                success(res) {
                    console.log(res.authSetting);
                }
            })
        }
    }
};
</script>

<style lang="less">
.about {
    width: 100%;
    .top_img {
        width: 100%;
        height: 320rpx;
        overflow: hidden;
        position: relative;
        image {
            width: 100%;
        }
    }
    .user {
        width: 80%;
        background: #ffffff;
        border-radius: 9px;
        display: flex;
        flex-flow: row nowrap;
        padding: 20rpx;
        position: absolute;
        top: 270rpx;
        left: 50%;
        transform: translateX(-50%);
        box-shadow: 1px 2px 5px 0px #eaeaea;
        image {
            display: block;
            flex: 0 0 130rpx;
            border-radius: 9rpx;
        }
        .name {
            flex: 1 1 auto;
            font-size: 32rpx;
            line-height: 130rpx;
            padding-left: 20rpx;
        }
        .setting {
            position: absolute;
            width: 50rpx;
            height: 50rpx;
            top: 20rpx;
            right: 20rpx;
            background: url(~@/static/ico/gerenicon-.png) no-repeat center;
            background-size: 100%;
        }
    }
}
</style>
