<template>
  <div class="side">
    <div class="side-top">
      <slide-tab :items="units" :active="unit" @change="changeUnit"/>
    </div>
    <div class="code-container" @click="setEditStatus(true)">
      <pre v-html="html" v-show="!editing"></pre>
      <textarea
        ref="textarea"
        :value="content"
        @input="changeContent"
        v-if="editable"
        v-show="editing"
        @blur="setEditStatus(false)"
      ></textarea>
    </div>
    <slot/>
  </div>
</template>
<script>
import SlideTab from "@/components/SlideTab";
import Prism from "prismjs";
const units = ["px", "em", "rem", "rpx"];
export default {
  model: {
    prop: "content",
    event: "changeContent"
  },
  components: {
    SlideTab
  },
  props: ["unit", "content", "editable"],
  data() {
    return {
      units,
      editing: false
    };
  },
  computed: {
    html() {
      return Prism.highlight(this.content, Prism.languages.css, 'css')
    }
  },
  watch: {
    unit() {
      this.editable&&this.changeContent();
    },
    editing(value) {
      if (value) {
        let area = this.$refs.textarea
        this.$nextTick(()=>{
          area.focus()
          area.select()
        })
      }
    }
  },
  methods: {
    setEditStatus(bool) {
      if (this.editable) {
        this.editing = bool
      }
    },
    changeUnit(e) {
      this.$emit("changeUnit", e);
    },
    changeContent() {
      const c = this.$refs.textarea.value;
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
  font-weight: 600;
  padding: 0 16px;
  cursor: pointer;
}
.tab-item:hover,
.active {
  color: #006aff;
}
.code-container {
  height: calc(100% - 80px);
  position: relative;
}
textarea, pre {
  display: block;
  font-family: 'monospace';
  white-space: pre;
  height: 100%;
  margin: 0;
  background-color: transparent;
  font-size: 14px;
  box-sizing: border-box;
  padding: 26px 24px;
  resize: none;
  width: 100%;
}
textarea {
  position: absolute;
  left: 0;
  top: 0;
}
</style>
