# vue-lottie-web

> a vue component for lottie-web

## Build Setup

``` bash

# use component
import Lottie from 'vue-lottie-web'

<Lottie
    className="animation" // to wapper dom class

    renderer="canvas | svg | html"
    :loop=boolean
    :autoplay=boolean
    :animationData=lottieData
    :path=lottieDataFilePath

    @getLottieInstance=getLottieInstance // get the lottie instence in parent component

    @onEnterFrame=onEnterFrame  // bind events
    @onComplete=onComplete
    @onLoopComplete=onLoopComplete
/>

```


