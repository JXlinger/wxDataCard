<script>
export default {
    globalData: {
        UserInfo: null,
        tableInfo: null,
        systemInfo: null
    },
    onLaunch: function() {
        const _self = this;
        if (this.globalData.UserInfo) {
            uni.switchTab({
                url: '/pages/index/index'
            });
        } else {
            uni.getUserInfo({
                success(res) {
                    _self.globalData.UserInfo = res.userInfo;
                }
            });
        }
    },
    onShow: function() {
        console.log(this.globalData);
    },
    onHide: function() {}
};
</script>

<style lang="less">
/*每个页面公共css */
</style>
