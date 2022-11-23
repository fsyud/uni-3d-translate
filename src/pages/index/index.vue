<template>
  <view class="content">
    <!-- <image class="logo" src="/static/logo.png" />
    <view class="text-area">
      <text class="title">{{ title }}</text>
    </view> -->
    <view class="container bg-dark-100">
      <view class="box">
        <view class="b-noodle a1">a1</view>
        <!-- 前 -->
        <view class="b-noodle a2">a2</view>
        <!-- 后 -->
        <view class="b-noodle b1">b1</view>
        <!-- 左 -->
        <view class="b-noodle b2">b2</view>
        <!-- 右 -->
        <view class="b-noodle c1">c1</view>
        <!-- 上 -->
        <view class="b-noodle c2">c2</view>
        <!-- 下 -->
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref } from "vue";
const title = ref("Hello");
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.container {
  height: 500px;
  background: #eee;
  perspective: 500px; /* 设置透视距离 */
}

/* x和y轴在屏幕上分别表现为左右和上下，z轴表示视觉上与我们的距离远近 */
.box {
  width: 200px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%) rotateZ(10deg) rotateX(-30deg);
  /* border: 1px solid #000; */
  transform-style: preserve-3d;
  animation: run 5s linear;
  animation-iteration-count: infinite;
}

.b-noodle {
  width: 200px;
  height: 200px;
  position: absolute;
  text-align: center;
  line-height: 200px;
  font-size: 30px;
}

.a1 {
  background: rgba(0, 0, 255, 0.5);
  transform: translateZ(100px);
}

.a2 {
  background: rgba(0, 0, 255, 0.5);
  transform: translateZ(-100px) rotateY(180deg);
}

.b1 {
  background: rgba(0, 255, 0, 0.5);
  transform: translateX(-100px) rotateY(-90deg);
}

.b2 {
  background: rgba(0, 255, 0, 0.5);
  transform: translateX(100px) rotateY(90deg);
}

.c1 {
  background: rgba(255, 0, 0, 0.5);
  transform: translateY(-100px) rotateX(90deg);
}

.c2 {
  background: rgba(255, 0, 0, 0.5);
  transform: translateY(100px) rotateX(-90deg);
}

@keyframes run {
  0% {
    transform: translate(-50%, -50%) rotateZ(10deg) rotateX(-30deg) rotateY(0);
  }
  50% {
    transform: translate(-50%, -50%) rotateZ(10deg) rotateX(-30deg)
      rotateY(180deg);
  }
  100% {
    transform: translate(-50%, -50%) rotateZ(10deg) rotateX(-30deg)
      rotateY(360deg);
  }
}
</style>
