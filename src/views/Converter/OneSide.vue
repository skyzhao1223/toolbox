<template>
  <div class="side">
    <div class="side-top">
      <slide-tab :items="units" :active="unit" @change="changeUnit"/>
    </div>
    <textarea
      ref="ta"
      :value="content"
      @input="$emit('changeContent',$event.target.value)"
      name
      id
      cols="30"
      rows="10"
    ></textarea>
    <slot/>
  </div>
</template>
<script>
import SlideTab from "@/components/SlideTab";
const units = ["px", "em", "rem", "rpx"];
export default {
  model: {
    prop: "content",
    event: "changeContent"
  },
  components: {
    SlideTab
  },
  props: ["unit", "content"],
  data() {
    return {
      units,
    };
  },
  watch: {
    unit() {
      this.changeContent();
    }
  },
  methods: {
    changeUnit(e) {
      this.$emit("changeUnit", e);
    },
    changeContent() {
      const c = this.$refs.ta.value;
      this.$emit("changeContent", c);
    }
  }
};
</script>
<style>
.side {
  float: left;
  width: 50%;
  height: 100%;
}
.side-top {
  border-bottom: 1px solid #e1e8ed;
  line-height: 80px;
}
.side-top .tab-item {
  text-transform: uppercase;
  display: inline-block;
  padding: 0 16px;
  cursor: pointer;
}
.active {
  color: #006aff;
}
textarea {
  background-color: transparent;
  font-size: 14px;
  box-sizing: border-box;
  height: calc(100% - 80px);
  padding: 26px 24px;
  resize: none;
  width: 100%;
}
</style>
