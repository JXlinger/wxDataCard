<template>
    <view class="user">
        <view class="top">制作你的名片</view>
        <form @submit="formSubmit" @reset="formReset">
            <view class="input_item input_name">
                <view>你的大名</view>
                <input v-model="tableInfo.name" type="text" maxlength="24" placeholder="名字" confirm-type="next" />
            </view>
            <view class="input_item input_sex">
                <label>帅气的男生</label>
                <switch v-model="tableInfo.sex" color="#ff3ae1" size @change="sexChange" style="transform:scale(0.7)"></switch>
                <label>可爱的女生</label>
            </view>
            <view class="input_item input_age">
                <slider
                    value="25"
                    block-size="20"
                    backgroundColor="rgb(239, 255, 0)"
                    activeColor="rgb(255, 23, 194)"
                    block-color="rgb(255, 23, 194)"
                    show-value
                    min="0"
                    max="80"
                    step="1"
                    v-model="tableInfo.age"
                />
                <view>岁</view>
            </view>
            <view class="input_item input_area">
                <view class="area_text">何处高就（{{ areaText }}）</view>
                <view class="area_input"><textarea v-model="tableInfo.corporation" maxlength="50" placeholder="公司名称" auto-height></textarea></view>
            </view>

            <view class="input_item input_area">
                <view class="area_text">BalaBala大道理</view>
                <view class="area_input"><textarea v-model="tableInfo.maxim" maxlength="200" placeholder="你的座右铭" auto-height></textarea></view>
            </view>
        </form>
    </view>
</template>

<script>
const app = getApp();
export default {
    data() {
        return {
            tableInfo: {
                name: '',
                sex: null,
                age: '',
                corporation: '',
                maxim: ''
            },
            corpArray: [
                "gou'qie'tou'sheng",
                "hun'shui'mo'yu",
                "xu'du'nian'hua",
                "lu'lu'wu'wei",
                "hun'hun'e'e",
                "de'guo'qie'guo",
                "wu'suo'shi'shi",
                "hun'chi'deng'si"
            ],
            areaText: ''
        };
    },
    onLoad() {
        console.log(app.globalData);
        var corpArray = this.corpArray;
        this.areaText = corpArray[Math.round(Math.random()*(corpArray.length-1))];
    },
    methods: {
        sexChange(e) {
            // console.log(e.target.value);
        }
    }
};
</script>

<style lang="less">
.user {
    width: 90%;
    height: 90%;
    position: fixed;
    background: #ffffff;
    border-radius: 15px;
    box-shadow: 0px 1px 10px 4px #ececec;
    top: 5%;
    left: 5%;
    background: url(~@/static/image/user_bg.jpg) top no-repeat;
    background-size: 100%;
    .top {
        padding: 50upx 0;
        text-align: center;
        font-size: 38upx;
        font-weight: 800;
    }
    form {
        display: block;
        width: 90%;
        margin: 30upx auto;
    }
    .input_item {
        width: 100%;
        height: 60upx;
        margin: 0 0 40upx 0;
    }
    .input_name {
        display: flex;
        flex-flow: row nowrap;
        view {
            font-size: 35upx;
            flex: 0 0 auto;
            line-height: 55upx;
            color: #ec3939;
            padding-right: 10upx;
        }
        input {
            display: block;
            padding-left: 20upx;
            flex: 1 1 auto;
            border-radius: 30px;
            background: rgba(255, 255, 255, 0.8);
            height: 100%;
            color: #2c405a;
        }
    }
    .input_sex {
        display: flex;
        switch {
            flex: 1;
        }
        label {
            font-size: 35upx;
            line-height: 60upx;
            color: #3aa5ff;
            flex: 1;
            text-align: center;
            &:last-child {
                color: #ff3ae1;
            }
        }
    }
    .input_age {
        display: flex;
        flex-flow: row nowrap;
        margin-right: 28upx;
        slider {
            flex: 1 1 auto;
            margin: 0 0 0 28upx !important;
        }

        view {
            flex: 0 0 auto;
            font-size: 30upx;
            color: #888;
        }
    }
    .input_area {
        height: auto;
        min-height: 60upx;
        .area_text {
            font-size: 35upx;
            color: #ec3939;
            padding: 0 0 10upx 10upx;
        }
        .area_input {
            padding: 20upx;
            border: 1px solid #f5f5f5;
            box-sizing: border-box;
            background: rgba(255, 255, 255, 0.8);
            border-radius: 15px;
            overflow: hidden;
        }
        textarea {
            width: auto;
        }
    }
}
</style>
