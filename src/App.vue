<template>
    <div id="app">
        <p class="pBtn">
            <span @click="lottiePlay">开始</span>
            <span @click="lottieRePlay">再一次</span>
            <span @click="lottiePause">暂停</span>
            <span @click="lottieStop">停止</span>
        </p>
        <Lottie
            className="animation"
            renderer="canvas"
            :loop="false"
            :autoplay="false"
            :animationData=lottieData

            @getLottieInstance=getLottieInstance
            @onEnterFrame=onEnterFrame
            @onComplete=onComplete
            @onLoopComplete=onLoopComplete
        />
    </div>
</template>

<script>
import Lottie from './VueLottieWeb/VueLottieWeb';
import lottieData from './assets/data.json';

export default {
    name: 'App',
    components: {
        Lottie
    },
    data() {
        return {
            lottieData,
            lottieInstance: ''
        };
    },

    methods: {
        getLottieInstance(lottieInstance) {
            this.lottieInstance = lottieInstance;

            console.log(lottieInstance)
        },
        lottiePlay() {
            this.lottieInstance && this.lottieInstance.play();
        },
        lottieRePlay() {
            this.lottieInstance && this.lottieInstance.stop();
            setTimeout(() => {
                this.lottieInstance.play();
            });
        },
        lottiePause() {
            this.lottieInstance && this.lottieInstance.pause();
        },
        lottieStop() {
            this.lottieInstance && this.lottieInstance.stop();
        },
        onComplete(e) {
            console.log('onComplete', e);
        },
        onLoopComplete(e) {
            console.log('onLoopComplete', e);
        },
        onEnterFrame(e) {
            // console.log('onEnterFrame', e);
        }
    }
};
</script>

<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
.pBtn span{
    display: inline-block;
    margin: 20px 30px;
    font-weight: bold;
}
.animation {
    background: #A0A0A0
}
</style>
