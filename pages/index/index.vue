<template>
	<view class="index">
		<view class="card_wrap">
            <view class="card_vat">
                <image mode="widthFix" src="../../static/image/card_img.jpg"></image>
            </view>
            <view class="card_info">
                <view>{{ tableInfo.name }}</view>
                <view>{{ tableInfo.sex == true ? '女' : '男' }} <text :class="tableInfo.sex == true ? 'women' : 'man'">{{ tableInfo.sex == true ? '♂' : '♀' }}</text></view>
                <view>{{ tableInfo.age }}</view>
                <view>{{ tableInfo.corporation }}</view>
                <view>{{ tableInfo.maxim }}</view>
            </view>
        </view>
        <view class="want_">
            <button open-type="getUserInfo" @getuserinfo="setTableInfo" size="mini" type="primary">我也要做名片</button>
        </view>
	</view>
</template>

<script>
    const app = getApp();
	export default {
		data() {
			return {
                tableInfo: {
                    has: true,
                    name: '春秋',
                    sex: true,
                    age: '24',
                    corporation: '阿里巴巴集团',
                    maxim: '我不是个随便的人，我随便起来不是人。'
                }
			}
		},
		onLoad() {
            
		},
        onShow() {
        },
		methods: {
            setTableInfo(e){
                console.log(e);
                app.globalData.UserInfo = e.detail.userInfo;
                uni.navigateTo({
                    url: '../user/index'
                })
            }
		}
	}
</script>

<style lang="less">
	.card_wrap{
        width: 90%;
        height: 80%;
        position: fixed;
        background: #FFFFFF;
        border-radius: 15px;
        box-shadow: 0px 1px 10px 4px #ececec;
        top: 50upx;
        left: 5%;
        background: url('~@/static/image/card_bg.jpg') no-repeat top;
        background-size: 100%;
        .card_vat{
            width: 300upx;
            height: 300upx;
            padding: 10upx;
            margin: 50upx auto;
            border-radius: 50%;
            overflow: hidden;
            background: url(~@/static/image/card_bg.jpg) center;
            background-size: 100%;
            image{
                width: 100%;
                border-radius: 50%;
            }
        }
        .card_info{
            text-align: center;
            padding: 20upx;
            view{
                font-size: 36upx;
                font-family: '华文新魏';
                line-height: 50upx;
                padding: 10upx 0;
                .women{
                    color: #ff3ae1;
                }
                .man{
                    color: #3aa5ff;
                }
                &:last-child{
                    text-align: left;
                    padding: 10px 50upx;
                }
            }
        }
    }
    .want_{
        position: fixed;
        bottom: 100upx;
        width: 100%;
        button{
            display: table;
            margin: 0 auto;
            font-size: 30upx;
        }
    }
</style>
