<template>
    <view class="creat">
        <view class="card_wrap">
            <view class="card_vat"><image mode="widthFix" :src="avatarUrl"></image></view>
            <view class="card_info">
                <view>{{ creatInfo.name }}</view>
                <view>
                    {{ creatInfo.sex == true ? '女' : '男' }}
                    <text :class="creatInfo.sex == true ? 'women' : 'man'">{{ creatInfo.sex == true ? '♂' : '♀' }}</text>
                </view>
                <view>{{ creatInfo.age }}</view>
                <view>{{ creatInfo.corporation }}</view>
                <view>{{ creatInfo.maxim }}</view>
            </view>
        </view>
    </view>
</template>

<script>
const app = getApp();
export default {
    data() {
        return {
            creatInfo: {},
            avatarUrl: require('../../static/image/card_img.jpg')
        };
    },
    onLoad() {
        console.log(app.globalData);
        if(app.globalData.tableInfo){
            this.creatInfo = app.globalData.tableInfo;
        }
        if(app.globalData.UserInfo){
            this.avatarUrl = app.globalData.UserInfo.avatarUrl
        }
        
    }
};
</script>

<style lang="less">
.card_wrap {
    width: 90%;
    height: 80%;
    position: fixed;
    background: #ffffff;
    border-radius: 15px;
    box-shadow: 0px 1px 10px 4px #ececec;
    top: 50upx;
    left: 5%;
    background: url('~@/static/image/card_bg.jpg') no-repeat top;
    background-size: 100%;
    .card_vat {
        width: 300upx;
        height: 300upx;
        padding: 10upx;
        margin: 50upx auto;
        border-radius: 50%;
        overflow: hidden;
        background: url(~@/static/image/card_bg.jpg) center;
        background-size: 100%;
        image {
            width: 100%;
            border-radius: 50%;
        }
    }
    .card_info {
        text-align: center;
        padding: 20upx;
        view {
            font-size: 36upx;
            font-family: '华文新魏';
            line-height: 50upx;
            padding: 10upx 0;
            .women {
                color: #ff3ae1;
            }
            .man {
                color: #3aa5ff;
            }
            &:last-child {
                // text-align: left;
                padding: 10px 50upx;
            }
        }
    }
}
</style>
