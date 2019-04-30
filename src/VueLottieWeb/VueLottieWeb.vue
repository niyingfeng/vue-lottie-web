<template>
    <div class="lottie" :class="className" ref="lottie"></div>
</template>

<script>
import lottie from 'lottie-web';

export default {
    data() {
        return {
            instance: false
        }
    },

    // 父级注册lottie动画参数
    // getLottieInstance 为子组件抛出动画对象的事件 由父组件获取使用
    props: {
        className: {
            type: String,
            default: ''
        },

        renderer: {
            type: String,
            default: 'canvas'
        },
        loop: {
            type: Boolean,
            default: true
        },
        autoplay: {
            type: Boolean,
            default: true
        },

        animationData: {
            type: Object | String,
            default: ''
        },
        path: {
            type: String,
            default: ''
        }
    },

    methods: {
        // 扩展方法
        extendMethods(instance) {
            // 自定义重播动画方法
            instance.customReplay = () => {
                instance.stop();
                setTimeout(() => {
                    instance.play();
                });
            }
        },
        // 透传注册事件
        transEvents(instance) {
            const events = ['onComplete', 'onLoopComplete', 'onEnterFrame', 'onSegmentStart'];

            events.forEach(keyName => {
                instance[keyName] = e => this.$emit(keyName, e);
            })
        }
    },

    mounted() {
        // 获取lottie参数 生成对象 并且扩展方法
        const {renderer, loop, autoplay, animationData, path} = this;

        const paramsInfo = {
            container: this.$refs.lottie,
            renderer,
            autoplay,
            loop
        }

        if (animationData) {
            paramsInfo.animationData = animationData;
        } else if (path) {
            paramsInfo.path = path;
        } else {
            throw new Error("Check Lottie Component's Props");
        }

        // lottie实例生成
        this.instance = lottie.loadAnimation(paramsInfo);

        // 自定义扩展方法与透传注册事件
        this.extendMethods(this.instance);
        this.transEvents(this.instance);

        // 抛出getLottieInstance事件 父节点获取动画对象
        this.$emit('getLottieInstance', this.instance);
    }
}
</script>

<style>
/*清除空节点照成canvas底部的空高度*/
.lottie {
    font-size: 0;
}
</style>