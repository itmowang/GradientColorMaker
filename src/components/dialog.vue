<!-- 弹框组件 -->
<template>
    <div>
        <div class="dialog-mask" v-show="show" @click="close"></div>
        <div class="dialog" v-show="show">
            <div class="dialog-header">
                <div class="dialog-title">{{ title }}</div>
                <div class="dialog-close" @click="close">X</div>
            </div>
            <div class="dialog-content">
                <slot></slot>
            </div>
            <div class="dialog-footer">
                <slot name="footer"></slot>
            </div>
        </div>
    </div>
</template>
<script setup>
import { ref, reactive, onMounted, defineProps, watch } from 'vue';
const emit = defineEmits(["close"])

const props = defineProps({
    title: {
        type: String,
        default: '提示'
    },
    show: {
        type: Boolean,
        default: false
    }
})

const close = () => {
    emit('close', false)
}




</script>
<style lang="less" scoped>
.dialog-mask {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 100;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, .5);
}

.dialog {
    position: fixed;
    top: 50%;
    left: 50%;
    z-index: 101;
    width: 500px;
    height: 300px;
    margin-left: -250px;
    margin-top: -150px;
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 0 10px rgba(0, 0, 0, .5);

    .dialog-header {
        height: 40px;
        line-height: 40px;
        padding: 0 10px;
        background-color: #eee;
        border-radius: 5px 5px 0 0;

        .dialog-title {
            float: left;
        }

        .dialog-close {
            float: right;
            cursor: pointer;
        }
    }

    .dialog-content {
        height: 220px;
        padding: 10px;
        overflow: auto;
    }

    .dialog-footer {
        height: 40px;
        line-height: 40px;
        padding: 0 10px;
        background-color: #eee;
        border-radius: 0 0 5px 5px;
    }
}</style>