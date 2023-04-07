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
    fillMode: 'attention'
  },
  {
    titel: '翻转效果',
    TypeList: overturn,
    fillMode: 'attention'
  },
  {
    titel: '旋转效果',
    TypeList: rotate,
    fillMode: 'attention'
  },
  {
    titel: '特殊效果',
    TypeList: special,
    fillMode: 'attention'
  },
  {
    titel: '弹跳出现效果',
    TypeList: dapAppear,
    fillMode: 'appear'
  },
  {
    titel: '弹跳消失效果',
    TypeList: dapVanish,
    fillMode: 'vanish'
  },
  {
    titel: '淡入淡出 出现效果',
    TypeList: fadAppear,
    fillMode: 'appear'
  },
  {
    titel: '淡入淡出 消失效果',
    TypeList: fadVanish,
    fillMode: 'vanish'
  },

  {
    titel: '急速出现效果',
    TypeList: quicknessAppear,
    fillMode: 'appear'
  },
  {
    titel: '急速消失效果',
    TypeList: quicknessVanish,
    fillMode: 'vanish'
  },
  {
    titel: '旋转出现效果',
    TypeList: rotateAppear,
    fillMode: 'appear'
  },
  {
    titel: '旋转消失效果',
    TypeList: rotateVanish,
    fillMode: 'vanish'
  },

  {
    titel: '放大缩小出现效果',
    TypeList: zoomAppear,
    fillMode: 'appear'
  },
  {
    titel: '放大缩小消失效果',
    TypeList: zoomVanish,
    fillMode: 'vanish'
  },
  {
    titel: '滑动出现效果',
    TypeList: slideAppear,
    fillMode: 'appear'
  },
  {
    titel: '滑动消失效果',
    TypeList: slideVanish,
    fillMode: 'vanish'
  }
]
const setAnimation = (animationType: string, fillMode: string = 'attention') => {
  // 获取HTML元素
  const element = document.querySelector(`#${animationType}-ani`) as HTMLDivElement
  // 若动画类型为出现，则移除透明类名（让元素显示）
  if (fillMode === 'appear') element.classList.remove('lucency');

  // 添加动画类名来触发动画效果
  element.classList.add(animationType);

  // 若动画类型为出现或消失，则显示最后一帧
  if (fillMode === 'appear' || fillMode === 'vanish') return

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
          <div :id="`${childItem}-ani`" class="animated" :class="{ lucency: item.fillMode === 'appear' }"
            :style="`background-image: ${background[childIndex]}`" @click="setAnimation(childItem, item.fillMode)"></div>
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

      &.lucency {
        opacity: 0;
      }
    }

    .name {
      font-size: 12px;
    }
  }
}
</style>
