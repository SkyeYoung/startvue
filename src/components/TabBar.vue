<template>
  <div id="head">
    <menu class="menu" ref="menu">
      <bar-item v-for="(v, i) in barItemList"
                :ref="setItemRef"
                :key="i"
                :item="v"
                @clickAction="clickItem(i)"
      />
      <div ref="menu_border" class="menu__border"/>
    </menu>

    <div class="svg-container">
      <svg viewBox="0 0 202.9 45.5">
        <clipPath
            id="menu"
            clipPathUnits="objectBoundingBox"
            transform="scale(0.0049285362247413 0.021978021978022)"
        >
          <path d="M6.7,45.5c5.7,0.1,14.1-0.4,23.3-4c5.7-2.3,9.9-5,18.1-10.5c10.7-7.1,11.8-9.2,20.6-14.3c5-2.9,9.2-5.2,15.2-7
            c7.1-2.1,13.3-2.3,17.6-2.1c4.2-0.2,10.5,0.1,17.6,2.1c6.1,1.8,10.2,4.1,15.2,7c8.8,5,9.9,7.1,20.6,14.3c8.3,5.5,12.4,8.2,18.1,10.5
            c9.2,3.6,17.6,4.2,23.3,4H6.7z"/>
        </clipPath>
      </svg>
    </div>

  </div>
</template>


<script>
import BarItem, {Item} from "@/components/BarItem";

export default {
  components: {
    BarItem
  },
  data() {
    return {
      barItemList: [
          new Item({
            bgColor: "#ffb457",
            paths: [
              "M3.8,6.6h16.4",
              "M20.2,12.1H3.8",
              "M3.8,17.5h16.4"
            ],
            active: true
          }),
          new Item({
            bgColor: "#ff96bd",
            paths: [
              "M6.7,4.8h10.7c0.3,0,0.6,0.2,0.7,0.5l2.8,7.3c0,0.1,0,0.2,0,0.3v5.6c0,0.4-0.4,0.8-0.8,0.8H3.8C3.4,19.3,3,19,3,18.5v-5.6c0-0.1,0-0.2,0.1-0.3L6,5.3C6.1,5,6.4,4.8,6.7,4.8z",
              "M3.4,12.9H8l1.6,2.8h4.9l1.5-2.8h4.6"
            ]
          }),
          new Item({
            bgColor: "#4343f5",
            paths:[
              "M3.4,11.9l8.8,4.4l8.4-4.4",
              "M3.4,16.2l8.8,4.5l8.4-4.5",
              "M3.7,7.8l8.6-4.5l8,4.5l-8,4.3L3.7,7.8z"
            ]
          }),
          new Item({
            bgColor: "#ffe797",
            paths: [
              "M5.1,3.9h13.9c0.6,0,1.2,0.5,1.2,1.2v13.9c0,0.6-0.5,1.2-1.2,1.2H5.1c-0.6,0-1.2-0.5-1.2-1.2V5.1C3.9,4.4,4.4,3.9,5.1,3.9z",
              "M4.2,9.3h15.6",
              "M9.1,9.5v10.3"
            ]
          }),
          new Item({
            bgColor: "#65ddb7",
            paths: [
              "M5.1,3.9h13.9c0.6,0,1.2,0.5,1.2,1.2v13.9c0,0.6-0.5,1.2-1.2,1.2H5.1c-0.6,0-1.2-0.5-1.2-1.2V5.1C3.9,4.4,4.4,3.9,5.1,3.9z",
              "M4.2,9.3h15.6",
              "M10.4,8.8c0,0.9-0.7,1.6-1.6,1.6c-0.9,0-1.6-0.7-1.6-1.6C7.3,8,8,7.3,8.9,7.3C9.7,7.3,10.4,8,10.4,8.8z"
            ]
          })
      ],
      last: 0,
      barItemRefList: []
    }
  },

  methods: {
    clickItem(index){
      console.log('done')
      this.barItemList[this.last].active = false
      this.barItemList[index].active = true
      this.setOffsetMenuBorder(this.barItemRefList[index].$refs.button)
      this.last = index;
    },
    setOffsetMenuBorder(activeItem) {
      const offsetActiveItem = activeItem.getBoundingClientRect();
      const left = Math.floor(
          offsetActiveItem.left - this.menu.offsetLeft -
          (this.menuBorder.offsetWidth - offsetActiveItem.width) / 2)
          + "px";
      this.menuBorder.style.transform = `translate3d(${left}, 0 , 0)`;
    },
    setItemRef(el){
      if(el){
        this.barItemRefList.push(el)
      }
    }
  },
  beforeUpdate() {
    this.barItemRefList = []
  },
  mounted() {
    this.menu = this.$refs.menu;
    this.menuBorder = this.$refs.menu_border;
    console.log()
  },
}
</script>

<style scoped>
#head {
  /*display: flex;*/
  justify-content: center;
  width: 100%;
  padding-top: 50px;
  box-sizing: border-box;
  --bgColorMenu: #1d1d27;
  --duration: .7s;
  font-size: 10px;
}


#head *,
#head *::before,
#head *::after {

  box-sizing: inherit;

}

.menu {
  margin: 0 auto;
  display: flex;
  /* Works well with 100% width  */
  width: 32.05em;
  font-size: 1.5em;
  padding: 0 2.85em;
  position: relative;
  align-items: center;
  justify-content: center;
  background-color: var(--bgColorMenu);

}

.menu__border {
  left: 0;
  bottom: 99%;
  width: 10.9em;
  height: 2.4em;
  position: absolute;
  clip-path: url(#menu);
  will-change: transform;
  background-color: var(--bgColorMenu);
  transition: transform .7s;

}

@media screen and (max-width: 50em) {
  .menu {
    font-size: .8em;
  }
}

.svg-container {

  width: 0;
  height: 0;
}
</style>
