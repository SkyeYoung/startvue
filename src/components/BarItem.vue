<template>
  <button
      ref="button"
      :class="['menu__item',{'active': active}]"
      :style="{'--bgColorItem': this.color}"
      @click="$emit('accepted')"
  >
    <svg class="icon" viewBox="0 0 24 24">
      <path v-for="[index, item] in path.entries()"
            :d="item"
            :key="index"
      />
    </svg>
  </button>
</template>

<script>

export default {
  name: "BarItem",
  props: {
    //barItem的背景色
    color: String,
    //是否处于选中（激活）状态
    active: Boolean,
    //barItem的SVG的路径
    path: Array,
    accepted: undefined
  },
  methods: {
    getRef() {
      return this.$refs.button;
    }
  }
}
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