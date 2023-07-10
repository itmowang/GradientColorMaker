<template>
    <div class="gradient">
        <div class="gradient-slider">
            <div class="gradient-slider-left" :class="state.currColor=='color1'?'gradient-slider-active':'' " ref="Color1Btn">
                <div class="gradient-slider-left-circle" :style="`background-color:${props.color1Data.color}`"></div>
            </div>
            <div class="slider" ref="slider"
                :style="`background:${getSliderGrdientCss(props.color1Data.color, props.color2Data.color)}`">
            </div>
            <div class="gradient-slider-right" :class="state.currColor=='color2'?'gradient-slider-active':'' " ref="Color2Btn">
                <div class="gradient-slider-right-circle" :style="`background-color:${props.color2Data.color}`"></div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref, reactive, onMounted, defineProps, watch } from 'vue';
const Color1Btn = ref(null);
const Color2Btn = ref(null);
const slider = ref(null);

const emit = defineEmits(["getGradient","getClickColor"])

const state = reactive({
    color1: '#FF0096',
    color2: '#FF0096',
    sliderWidth: 600,
    sliderInitLeftPosition: 0, // 记录初始位置
    sliderLeftPosition: 0, // 记录左边按钮位置
    sliderInitRigtPosition: 0, // 记录初始位置
    sliderRightPosition: 600, // 记录右边按钮位置
    bgGrdientCss: "",
    currColor: "color1"
})

const props = defineProps({
    color1Data: {
        type: Object,
        default: {
            color: "#95ECB0",
            postion: 0,
            rotaion: 0,
            type: "linear",
        }
    },
    color2Data: {
        type: Object,
        default: {
            color: "#F3F98A",
            postion: 600,
            rotaion: 0,
            type: "linear",
        }
    },
})

// 监听getSliderGrdientCss函数返回值的变化wath emit给父组件
watch(() => state.bgGrdientCss, (newVal, oldVal) => {
    emit('getGradient', newVal)
})

//监听props.color1Data.postion 百分比的变化 并计算改变当前滚动按钮的位置
watch(() => props.color1Data.postion, (newVal, oldVal) => {
    // 计算当前滚动按钮的位置
    const left = (newVal / 100) * state.sliderWidth;
    // 设置当前滚动按钮的位置
    Color1Btn.value.style.left = `${left}px`;
    // 设置slider的渐变色
    slider.value.style.background = getSliderGrdientCss(props.color1Data.color, props.color2Data.color);
})

//监听props.color2Data.postion 百分比的变化 并计算改变当前滚动按钮的位置
watch(() => props.color2Data.postion, (newVal, oldVal) => {
    // 计算当前滚动按钮的位置
    const left = (newVal / 100) * state.sliderWidth;
    // 设置当前滚动按钮的位置
    Color2Btn.value.style.left = `${left}px`;
    // 设置slider的渐变色
    slider.value.style.background = getSliderGrdientCss(props.color1Data.color, props.color2Data.color);
})

// 监听state.currColor 告诉父级是哪个按钮被点击
watch(() => state.currColor, (newVal, oldVal) => {
    emit('getClickColor', newVal)
})

const getSliderGrdientCss = (color1, color2) => {
    // const gradient = `linear-gradient(to right, ${color1}, ${color2})`;
    // 加入postion 生成的渐变色
    // const gradient = `linear-gradient(to right, ${color1} ${props.color1Data.postion}%, ${color2} ${props.color2Data.postion}%)`;
    // 加入postion 加入rotaion 生成的渐变色 
    // const gradient = `linear-gradient(${props.color1Data.rotaion}deg, ${color1} ${props.color1Data.postion}%, ${color2} ${props.color2Data.postion}%)`;
    // 加入postion 加入rotaion 加入type分为linear radial  生成的渐变色
    const gradient = `${props.color1Data.type}-gradient(${props.color1Data.rotaion}deg, ${color1} ${props.color1Data.postion}%, ${color2} ${props.color2Data.postion}%)`;
    state.bgGrdientCss = gradient;
    return gradient
}

// 根据当前滚动条的位置计算postion渐变占比为百分之多少
const getPostion = (left) => {
    // 超过sliderWidth的部分不计算
    if (left > state.sliderWidth) {
        return 100
    }
    // 小于0的部分不计算
    if (left < 0) {
        return 0
    }
    return (left / state.sliderWidth) * 100
}

// 鼠标按下的事件Left
const dragStartLeft = (event) => {
    // 记录左边按钮初始位置
    state.sliderInitLeftPosition = event.clientX;
    // 根据sliderWidth 记录位置
    state.sliderLeftPosition = Color1Btn.value.offsetLeft;
    // 添加鼠标移动和鼠标释放的事件监听
    document.addEventListener('mousemove', dragLeftMove)
    document.addEventListener('mouseup', dragEndLeft)
    // 告诉父组件是Color被点击
    state.currColor = "color1"
}
// 鼠标移动的事件
const dragLeftMove = (event) => {
    // 计算拖动距离
    const dragDistance = event.clientX - state.sliderInitLeftPosition;
    // 更新按钮位置
    Color1Btn.value.style.left = `${state.sliderLeftPosition + dragDistance}px`;
    // 更新postion
    props.color1Data.postion = getPostion(Color1Btn.value.offsetLeft);
    // 不让超出
    if (Color1Btn.value.offsetLeft < 0) {
        Color1Btn.value.style.left = 0;
    }
    if (Color1Btn.value.offsetLeft > state.sliderRightPosition) {
        Color1Btn.value.style.left = `${state.sliderRightPosition}px`;
    }
};
 
// 释放
const dragEndLeft = (event) => {
    // 移除事件监听
    document.removeEventListener('mousemove', dragLeftMove)
    document.removeEventListener('mouseup', dragEndLeft)
}

// 鼠标按下的事件Right
const dragStartRight = (event) => {
    // 记录右边按钮初始位置
    state.sliderInitRigtPosition = event.clientX;
    // 根据sliderWidth 记录位置
    state.sliderRightPosition = Color2Btn.value.offsetLeft;
    // 添加鼠标移动和鼠标释放的事件监听
    document.addEventListener('mousemove', dragRightMove)
    document.addEventListener('mouseup', dragEndRight)
    // 告诉父组件是Color被点击
    state.currColor = "color2"
}
const dragRightMove = (event) => {
    // 计算拖动距离
    const dragDistance = event.clientX - state.sliderInitRigtPosition;
    // 更新按钮位置
    Color2Btn.value.style.left = `${state.sliderRightPosition + dragDistance}px`;
    // 更新postion
    props.color2Data.postion = getPostion(Color2Btn.value.offsetLeft);
    // 不让超出
    if (Color2Btn.value.offsetLeft < state.sliderLeftPosition) {
        Color2Btn.value.style.left = `${state.sliderLeftPosition}px`;
    }
    if (Color2Btn.value.offsetLeft > state.sliderWidth) {
        Color2Btn.value.style.left = `${state.sliderWidth}px`;
    }
}
// 释放
const dragEndRight = (event) => {
    // 移除事件监听
    document.removeEventListener('mousemove', dragRightMove)
    document.removeEventListener('mouseup', dragEndRight)
}

onMounted(() => {
    Color1Btn.value.addEventListener('mousedown', dragStartLeft)
    Color2Btn.value.addEventListener('mousedown', dragStartRight)
})


</script>
<style lang="less" scoped>
.gradient {
    .gradient-slider {
        position: relative;

        .slider {
            background-color: #f7f7f8;
            height: 20px;
            box-shadow: inset rgba(0, 0, 0, 0.075) 0 0 0 1px;
            border-radius: 10px;
        }

        .gradient-slider-left {
            width: 25px;
            height: 25px;
            border: 1px solid #e6e6e6;
            border-radius: 50%;
            background-color: #FFF;
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);

            .gradient-slider-left-circle {
                width: 15px;
                height: 15px;
                border-radius: 50%;
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                border: 1px solid #e6e6e6;
            }
        }

        .gradient-slider-right {
            width: 25px;
            height: 25px;
            border: 1px solid #e6e6e6;
            border-radius: 50%;
            background-color: #FFF;
            position: absolute;
            right: 0;
            top: 50%;
            transform: translateY(-50%);

            .gradient-slider-right-circle {
                width: 15px;
                height: 15px;
                border-radius: 50%;
                position: absolute;
                left: 50%;
                top: 50%;
                transform: translate(-50%, -50%);
                border: 1px solid #e6e6e6;
            }
        }
        .gradient-slider-active{
            border-color: #1890ff;
        }
    }
}
</style>