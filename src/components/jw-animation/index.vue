
<script lang="ts">
export default {
  name: 'jwAnimation'
} 
</script>
<script lang="ts" setup>
import { background } from './const/backgroundColor'
import {
  attention,
  dapAppear,
  dapVanish,
  fadAppear,
  fadVanish,
  overturn,
  quicknessAppear,
  quicknessVanish,
  rotate,
  rotateAppear,
  rotateVanish,
  special,
  zoomAppear,
  zoomVanish,
  slideAppear,
  slideVanish
} from './const/animationType'
const animationTypeList = [
  {
    titel: '引起注意效果',
    TypeList: attention,
    fillMode: 'backwards'
  },
  {
    titel: '弹跳出现效果',
    TypeList: dapAppear,
    fillMode: 'backwards'
  },
  {
    titel: '弹跳消失效果',
    TypeList: dapVanish,
    fillMode: 'forwards'
  },
  {
    titel: '淡入淡出 出现效果',
    TypeList: fadAppear,
    fillMode: 'backwards'
  },
  {
    titel: '淡入淡出 消失效果',
    TypeList: fadVanish,
    fillMode: 'forwards'
  },
  {
    titel: '翻转效果',
    TypeList: overturn,
    fillMode: 'backwards'
  },
  {
    titel: '急速出现效果',
    TypeList: quicknessAppear,
    fillMode: 'backwards'
  },
  {
    titel: '急速消失效果',
    TypeList: quicknessVanish,
    fillMode: 'forwards'
  },
  {
    titel: '旋转效果',
    TypeList: rotate,
    fillMode: 'backwards'
  },
  {
    titel: '旋转出现效果',
    TypeList: rotateAppear,
    fillMode: 'backwards'
  },
  {
    titel: '旋转消失效果',
    TypeList: rotateVanish,
    fillMode: 'forwards'
  },
  {
    titel: '特殊效果',
    TypeList: special,
    fillMode: 'backwards'
  },
  {
    titel: '放大缩小出现效果',
    TypeList: zoomAppear,
    fillMode: 'backwards'
  },
  {
    titel: '放大缩小消失效果',
    TypeList: zoomVanish,
    fillMode: 'forwards'
  },
  {
    titel: '滑动出现效果',
    TypeList: slideAppear,
    fillMode: 'backwards'
  },
  {
    titel: '滑动消失效果',
    TypeList: slideVanish,
    fillMode: 'forwards'
  }
]
const setAnimation = (animationType: string, fillMode: string = 'backwards') => {
  // 获取HTML元素
  const element = document.querySelector(`#${animationType}-ani`) as HTMLDivElement

  // 添加动画类名来触发动画效果
  element.classList.add(animationType);

  // 若动画类型为消失，则显示最后一帧
  // if (fillMode === 'forwards') return

  // 监听动画结束事件，当动画结束时执行回调函数
  element.addEventListener('animationend', function animationEndCallback() {
    // 将动画类名从元素上移除
    element.classList.remove(animationType);

    // 取消监听事件，以避免事件重复触发
    element.removeEventListener('animationend', animationEndCallback);
  });
}
</script>

<template>
  <div class="main">
    <div style="margin-bottom: 100px;" v-for="(item, index) in animationTypeList" :key="index">
      <p class="title">{{ item.titel }}</p>
      <div class="collection">
        <div class="item-body" v-for="(childItem, childIndex) in item.TypeList" :key="childIndex">
          <div :id="`${childItem}-ani`" class="animated" :style="`background-image: ${background[childIndex]}`"
            @click="setAnimation(childItem, item.fillMode)"></div>
          <span class="name">{{ childItem }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import './css/index.css';

.main {
  width: 1000px;
  margin: 0 auto;
}

.title {
  font-size: 20px;
  font-weight: 700;
}

.collection {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  row-gap: 40px;
  column-gap: 100px;

  .item-body {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;

    .animated {
      width: 120px;
      height: 70px;
      border-radius: 8px;
    }

    .name {
      font-size: 12px;
    }
  }
}
</style>
