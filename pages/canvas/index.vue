<template>
    <view class="canvas">
        <view class="card_wrap"><canvas canvas-id="creatImg" style="width: 100%;height: 100%"></canvas></view>
        <view class="setimg">
            <button type="primary" @tap="saveCanvasImg">保存图片</button>
            <button type="primary" open-type="share">分享</button>
        </view>
    </view>
</template>

<script>
const app = getApp();
export default {
    data() {
        return {
            tableInfo: {},
            avatarUrl: require('../../static/image/card_img.jpg'),
            canvasW: 100,
            canvasH: 100,
            drawLineX: 165,
            drawLineY: 220,
            drawLineNext: 250,
            address: '',
            finished: false
        };
    },
    onLoad() {
        
        console.log(app.globalData);
        if(app.globalData.tableInfo){
            this.tableInfo = app.globalData.tableInfo
        }
        if(app.globalData.UserInfo){
            this.avatarUrl = app.globalData.UserInfo.avatarUrl
            console.log(this.avatarUrl);
        }
        this.canvasW = uni.getSystemInfoSync().windowWidth;
        this.canvasH = uni.getSystemInfoSync().windowHeight;
        this.toDrawCanvas();
    },
    methods: {
        saveCanvasImg() {
            if (!this.finished) {
                uni.showToast({
                    title: '正在生成图片，稍后再试',
                    icon: 'none'
                });
                return;
            }
            const that = this;
            uni.canvasToTempFilePath({
                canvasId: 'creatImg',
                success: res => {
                    uni.saveImageToPhotosAlbum({
                        filePath: res.tempFilePath,
                        success: () => {
                            uni.showToast({
                                icon: 'success',
                                title: '保存成功',
                                duration: 2000
                            });
                        },
                        fail() {
                            uni.showToast({
                                icon: 'none',
                                title: '相册权限禁止，请在设置中打开',
                                duration: 1500
                            });
                            
                        }
                    });
                },
                fail() {
                    uni.showToast({
                        icon: 'none',
                        title: '保存失败，请重新保存'
                    });
                }
            });
        },
        async toDrawCanvas() {
            const padding = uni.upx2px(34);
            const cardHeight = uni.upx2px(600);

            const ctx = uni.createCanvasContext('creatImg', this);
            ctx.setFillStyle('#FFFFFF');
            ctx.fillRect(0, 0, this.canvasW, this.canvasH);
            this.toDrawImage(ctx, padding);

            this.toDrawText(ctx, padding);
            this.toDrawQrcode(ctx, padding);
            ctx.draw();
            this.finished = true;
        },
        async toDrawImage(ctx, padding) {
            //绘制背景图
            ctx.drawImage('../../static/image/card_bg.jpg', 0, 0, this.canvasW - padding * 2, uni.upx2px(800), 0, 0);
            //绘制头像
            ctx.drawImage(app.globalData.UserInfo.avatarUrl, this.canvasW - this.canvasW / 2 - 60 - padding, 40, 120, 120, 0, 0);
        },
        async toDrawQrcode(ctx, padding) {
            //绘制二维码这块 这块坐标是估的 哈哈哈~~~
            ctx.drawImage('../../static/image/Qr_code.png', this.drawLineX + padding * 2, this.drawLineNext * 1.5 + padding * 3, 100, 100, 0, 0);
        },
        async toDrawText(ctx, padding) {
            let textAlignX = this.drawLineX;
            let textAlignY = this.drawLineY;
            let textAlignNext = this.drawLineNext;

            ctx.setFontSize(18);
            ctx.setFillStyle('#2b2b2b');
            ctx.setTextAlign('center');
            ctx.fillText(this.tableInfo.name, textAlignX, textAlignY);
            ctx.fillText(this.tableInfo.sex == false ? '男' : '女', 155, textAlignNext);
            ctx.fillText(this.tableInfo.age, textAlignX, textAlignNext + 30);
            ctx.fillText(this.tableInfo.corporation, textAlignX, textAlignNext + 30 * 2);
            var filltext = this.tableInfo.maxim;
            this.textDrawLine(ctx, filltext, padding, textAlignX, textAlignY);
            ctx.setFillStyle(this.tableInfo.sex == false ? '#3aa5ff' : '#ff3ae1');
            ctx.fillText(this.tableInfo.sex == false ? '♂' : '♀', 175, textAlignNext);
            // ctx.fillText('textAlign=left', 150, 60)
        },
        textDrawLine(ctx, filltext, padding, x, y) {
            // 文字换行操作
            let chr = filltext.split('');
            let temp = '';
            let row = [];
            const ys = 3 * 30 + y;
            for (let a = 0; a < chr.length; a++) {
                if (ctx.measureText(temp).width < this.canvasW - padding * 2 && ctx.measureText(temp + chr[a]).width <= this.canvasW - padding * 2) {
                    temp += chr[a];
                } else {
                    row.push(temp);
                    temp = chr[a];
                }
            }
            row.push(temp);
            for (let b = 0; b < row.length; b++) {
                ctx.fillText(row[b], x, ys + (b + 1) * 30); //每行字体y坐标间隔20
            }
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
    overflow: hidden;
}
.setimg {
    position: fixed;
    display: flex;
    bottom: 100upx;
    width: 100%;
    button {
        width: 30%;
        font-size: 30upx;
    }
}
</style>
