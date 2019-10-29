<template>
    <view class="user">
        <view class="top">制作你的名片</view>
        <form @submit="formSubmit">
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
                    @change="sliderChange"
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
            <view class="submit">
                <button type="primary" size="default" @tap="toCreatCanvas">生成图片名片</button>
                <button type="primary" size="default" @tap="toCreatCard">生成普通名片</button>
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
        if(!this.tableInfo.sex){
            this.tableInfo.sex = false
        }
        if(!this.tableInfo){
            this.tableInfo.has = false
        }else{
            this.tableInfo.has = true
        }
        var corpArray = this.corpArray;
        this.areaText = corpArray[Math.round(Math.random()*(corpArray.length-1))];
    },
    methods: {
        sexChange(e) {
             this.tableInfo.sex = e.target.value
        },
        sliderChange(e){
            this.tableInfo.age = e.target.value
        },
        formVerification(){},
        toCreatCanvas(e){
            if(!this.tableInfo.name){
                uni.showToast({
                    title: '叫火云邪神也行啊！',
                    image: '../../static/image/mei_ming_zi.jpg',
                    duration: 3000
                });
                return;
            }else if(this.tableInfo.age < 6 || !this.tableInfo.age){
                uni.showToast({
                    title: '你还没到6岁？',
                    image: '../../static/image/child_can_not_play_phone.jpg',
                    duration: 3000
                });
                return;
            }else if(!this.tableInfo.corporation){
                uni.showToast({
                    image: '../../static/image/yaseiyalai.jpg',
                    title: '写个精神病院吧！',
                    duration: 3000
                })
                return;
            }else if(!this.tableInfo.maxim){
                uni.showToast({
                    image: '../../static/image/yaseiyalai.jpg',
                    title: '吹个牛逼也不会？',
                    duration: 3000
                })
                return;
            }else{
                app.globalData.tableInfo = this.tableInfo;
                let times = Math.floor(1500 + Math.random()*4000);
                uni.showLoading({
                    title: '正在生成中...',
                    success() {
                        setTimeout(() => {
                           uni.navigateTo({
                               url: '../canvas/index',
                               success() {
                                  uni.hideLoading();
                               }
                           }) 
                        },times)
                        
                    }
                })
            }
                
        },
        toCreatCard(){
            if(!this.tableInfo.name){
                uni.showToast({
                    title: '叫火云邪神也行啊！',
                    image: '../../static/image/mei_ming_zi.jpg',
                    duration: 3000
                });
                return;
            }else if(this.tableInfo.age < 6 || !this.tableInfo.age){
                uni.showToast({
                    title: '你还没到6岁？',
                    image: '../../static/image/child_can_not_play_phone.jpg',
                    duration: 3000
                });
                return;
            }else if(!this.tableInfo.corporation){
                uni.showToast({
                    image: '../../static/image/yaseiyalai.jpg',
                    title: '写个精神病院吧！',
                    duration: 3000
                })
                return;
            }else if(!this.tableInfo.maxim){
                uni.showToast({
                    image: '../../static/image/yaseiyalai.jpg',
                    title: '吹个牛逼也不会？',
                    duration: 3000
                })
                return;
            }else{
                let times = Math.floor(1500 + Math.random()*4000);
                app.globalData.tableInfo = this.tableInfo;
                uni.showLoading({
                    title: '正在生成中...',
                    success() {
                        setTimeout(() => {
                           uni.navigateTo({
                               url: '../creat/index',
                               success() {
                                  uni.hideLoading();
                               }
                           }) 
                        },times)
                        
                    }
                })
            }
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
    .submit{
        width: 100%;
        position: absolute;
        bottom: 30upx;
        left: 50%;
        transform: translateX(-50%);
        button{
            transform: scale(.9);
            background: rgba(255,185,41);
            color: #FFFFFF;
            &:last-child{
                background: #4CD964;
                margin-top: 10upx;
            }
        }
        
    }
}
</style>
