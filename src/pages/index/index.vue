<template>
  <view class="content">
    <view>{{ initDeg }}</view>
    <view class="container bg-dark-100">
      <view
        class="box"
        @touchstart="startDrag"
        @touchmove="moveDrag"
        :style="{
          transform: `translate(-50%, -50%) rotateZ(0) rotateX(-10deg) rotateY(${initDeg}deg)`,
          background: 'red',
        }"
      >
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

const initDeg = ref<number>(0);
const initStartDeg = ref<number>(0);

const startDrag = (event: any): any => {
  initStartDeg.value = event.touches[0].clientX;
};

const moveDrag = (event: any) => {
  let currentTouchX = event.touches[0].clientX;
  initDeg.value = currentTouchX - initStartDeg.value;
};
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.container {
  height: 300px;
  perspective: 500px; /* 设置透视距离 */
  position: absolute;
  top: 0;
  animation: containMove 0.5s ease-in;
}

/* x和y轴在屏幕上分别表现为左右和上下，z轴表示视觉上与我们的距离远近 */
.box {
  width: 160px;
  position: absolute;
  left: 50%;
  top: 50%;
  /* transform: translate(-50%, -50%) rotateY(-10deg); */
  /* border: 1px solid #000; */
  transform-style: preserve-3d;
  animation: run 2.5s ease-out;
  /* animation-iteration-count: infinite; */
  /* 动画终止 */
  /* animation-fill-mode: forwards; */
}


.b-noodle {
  width: 160px;
  height: 160px;
  position: absolute;
  text-align: center;
  line-height: 160px;
  font-size: 30px;
}

.a1 {
  background: #a82dff;
  transform: translateZ(80px);
}

.a2 {
  background: #504ad9;
  transform: translateZ(-80px) rotateY(180deg);
}

.b1 {
  background: #5da4f0;
  transform: translateX(-80px) rotateY(-90deg);
}

.b2 {
  background: #d98c4a;
  transform: translateX(80px) rotateY(90deg);
}

.c1 {
  background: #61faa3;
  transform: translateY(-80px) rotateX(90deg);
}

.c2 {
  background: #facf61;
  transform: translateY(80px) rotateX(-90deg);
}

@keyframes containMove {
  from {
    right: -50%;
  }
  to {
    right: 50%;
  }
}

@keyframes run {
  0% {
    transform: translate(-50%, -50%) rotateZ(0) rotateX(-10deg) rotateY(0);
  }
  25% {
    transform: translate(-50%, -50%) rotateZ(0) rotateX(-10deg) rotateY(360deg);
  }
  50% {
    transform: translate(-50%, -50%) rotateZ(0) rotateX(-10deg) rotateY(0deg);
  }
  100% {
    transform: translate(-50%, -50%) rotateZ(0) rotateX(-10deg) rotateY(360deg);
  }
}
</style>
