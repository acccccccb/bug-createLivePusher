<template>
    <view class="content">
        <image class="logo" src="/static/logo.png"></image>
        <view class="text-area">
            <button @click="testCamera" class="title">
                开启摄像头 3秒后关闭
            </button>
        </view>
    </view>
</template>

<script>
export default {
    data() {
        return {
            title: 'Hello',
        };
    },
    onLoad() {},
    methods: {
        testCamera() {
            console.log('testCamera');
            let camera = null;
            const currentWebview = this.$mp.page.$getAppWebview();

            camera = plus.video.createLivePusher('camera', {
                url: '',
                top: '50%',
                left: '30%',
                width: '40%',
                height: '200px',
                position: 'static',
                orientation: 'vertical',
                optimize: false,
                muted: true,
            });

            camera.addEventListener(
                'statechange',
                () => {
                    console.log('statechange', statechange);
                },
                false
            );

            currentWebview.append(camera);

            setTimeout(() => {
                camera.close();
            }, 3000);
        },
    },
};
</script>

<style>
.content {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.logo {
    height: 200rpx;
    width: 200rpx;
    margin-top: 200rpx;
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 50rpx;
}

.text-area {
    display: flex;
    justify-content: center;
}

.title {
    font-size: 36rpx;
    color: #8f8f94;
}
</style>
