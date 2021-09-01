<template>
  <button
    ref="button"
    :class="['menu__item',{'active': item.active}]"
    :style="{'--bgColorItem': item.bgColor}"
    @click="$emit('clickAction')"
  >
    <svg
      class="icon"
      viewBox="0 0 24 24"
    >
      <path
        v-for="(v, i) in item.paths"
        :key="i"
        :d="v"
      />
    </svg>
  </button>
</template>

<script lang="ts">
import {defineComponent} from "vue";

export interface ItemInter {
  /**
   * 背景色
   */
 bgColor: string;
  /**
   * SVG 路径
   */
 paths: string[];
  /**
   * 是否激活
   */
 active?: boolean
}

export class Item implements ItemInter{
  bgColor: string;
  paths: string[];
  active: boolean;

  constructor(props: ItemInter) {
    this.bgColor = props.bgColor
    this.paths = props.paths
    this.active = props.active || false
  }
}

export default defineComponent({
  props: {
    item: {
      type: Item,
      required: true
    },
  },
  emits: ['clickAction'],
})
</script>

<style scoped>
.menu__item{

  all: unset;
  flex-grow: 1;
  z-index: 100;
  display: flex;
  cursor: pointer;
  position: relative;
  border-radius: 50%;
  align-items: center;
  will-change: transform;
  justify-content: center;
  padding: 0.55em 0 0.85em;
}

.menu__item::before{

  content: "";
  z-index: -1;
  width: 4.2em;
  height: 4.2em;
  border-radius: 50%;
  position: absolute;
  transform: scale(0);
  transition: background-color var(--duration), transform var(--duration);
}

.menu__item.active {

  transform: translate3d(0, -.8em , 0);

}

.menu__item.active::before{

  transform: scale(1);
  background-color: var(--bgColorItem);

}

.icon{

  width: 2.6em;
  height: 2.6em;
  stroke: white;
  fill: transparent;
  stroke-width: 1pt;
  stroke-miterlimit: 10;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke-dasharray: 400;

}

.menu__item.active .icon {

  animation: strok 1.5s reverse;

}

@keyframes strok {

  100% {

    stroke-dashoffset: 400;

  }

}

</style>
