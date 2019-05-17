# vue-lottie-web

> a vue component for lottie-web

## Demo Show

show Demo in local:

```
git clone git@github.com:niyingfeng/vue-lottie-web.git

npm install

npm run dev
```

## Component use

Install through npm:

```
npm install --save vue-lottie-web
```

``` bash
# use component
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
import Lottie from 'vue-lottie-web';
import lottieData from './data.json';

export default {
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


```


