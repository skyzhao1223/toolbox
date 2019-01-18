<template>
  <div class="tab slide">
    <div
      class="tab-item"
      :class="{
        active: item === active
      }"
      v-for="(item, index) in items"
      :key="index"
      :ref="index"
      @click="$emit('change',item)"
    >{{item}}</div>
    <div class="active-line" :style="{left:`${posX}px`,width:`${width}px`}"></div>
  </div>
</template>
<script>
export default {
  props: ["items", "active"],
  data() {
    return {
      lenArr: [],
      width: 0,
      posX: 0
    };
  },
  watch: {
    active(item) {
      this.setActive(item)
    }
  },
  mounted() {
    this.init();
  },
  methods: {
    init() {
      const keys = Object.keys(this.$refs);
      const len = keys.length;
      for (let i = 0; i < len; i++) {
        const l = this.$refs[i][0].offsetWidth;
        this.lenArr.push(l);
      }
      this.setActive(this.active)
    },
    setActive(item) {
      const p = this.items.indexOf(item)
      let posX = 0
      for (let i = 0; i < p; i++) {
        posX += this.lenArr[i]
      }
      this.posX = posX
      this.width = this.lenArr[p]
    }
  }
};
</script>
<style scoped>
.tab {
  position: relative;
}
.tab-item {
  display: inline-block;
}
.active-line {
  height: 2px;
  min-width: 32px;
  display: inline-block;
  background-color: #006aff;
  position: absolute;
  transition: 250ms;
  bottom: -1px;
  left: 0;
}
</style>
