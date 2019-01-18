<template>
  <div id="converter">
    <one-side :unit="from" v-model="origin" @changeUnit="changeFrom" @changeContent="changeContent">
      <div class="ratio-setter">
        <div class="clear-btn hover">
          <div class="hover-text">Clear</div>
        </div>
        <b>1</b>
        {{to}} =
        <input v-model="ratio">
        {{from}}
      </div>
    </one-side>
    <one-side class="reverse" :unit="to" :content="result" @changeUnit="changeTo">
      <div class="ratio-setter">
        <div class="copy-btn hover">
          <div class="hover-text">Copy Code</div>
        </div>
        <b>1</b>
        {{from}} =
        <input v-model="ratioReverse">
        {{to}}
      </div>
    </one-side>
    <div class="center">
      <div class="center-btn" :class="{flip}" @click="reverse"></div>
      <div class="center-line"></div>
    </div>
  </div>
</template>
<script>
import OneSide from "./OneSide";
export default {
  components: {
    OneSide
  },
  data() {
    return {
      from: "px",
      to: "rem",
      ratio: 1 / 16,
      origin: "20px 20rem",
      result: "",
      flip: false
    };
  },
  computed: {
    resultFilter: {
      get() {
        return this.result;
      },
      set(value) {
        return value;
      }
    },
    ratioReverse: {
      get() {
        return 1 / this.ratio;
      },
      set(value) {
        this.ratio = 1 / value;
      }
    }
  },
  watch: {
    ratio() {
      this.changeContent();
    }
  },
  methods: {
    changeFrom(unit) {
      this.from = unit;
      this.changeContent();
    },
    changeTo(unit) {
      this.to = unit;
      this.changeContent();
    },
    reverse() {
      if (!this.flip) {
        const flip = () => {
          this.flip = true;
          setTimeout(() => {
            this.flip = false;
          }, 250);
        };
        flip();
        const to = this.to;
        this.changeTo(this.from);
        this.changeFrom(to);
      }
    },
    changeContent() {
      const originType = this.from.toLowerCase();
      const targetType = this.to.toLowerCase();
      const reg = new RegExp(`\\d+[.]*[\\d]*${originType}`, "gi");
      let content = this.origin;
      const arr = content.match(reg) || [];
      arr.forEach(e => {
        const eachResult = parseFloat(e) / this.ratio + targetType;
        content = content.replace(e, eachResult);
      });
      this.result = content;
      // console.log(this.origin, originType, targetType, arr, this.result);
    }
  },
  mounted() {
    this.changeContent();
  }
};
</script>
<style>
#converter {
  height: calc(100vh - 206px);
  background: linear-gradient(180deg, white, #f8fafc);
  box-sizing: border-box;
  padding: 0 24px 26px;
  position: relative;
}
#converter .side {
  position: relative;
}
#converter .ratio-setter {
  background-color: #f3f6f8;
  padding: 4px 12px;
  position: absolute;
  color: #9aa7b9;
  right: 23px;
  top: 104px;
}
#converter .ratio-setter b,
#converter .ratio-setter input {
  color: #4a4a4a;
}
#converter .ratio-setter input {
  border: 1px solid #e1e8ed;
  box-sizing: border-box;
  font-size: 14px;
  line-height: 1.571428571;
  text-align: center;
  height: 22px;
  width: 48px;
}
#converter .ratio-setter [class*="btn"] {
  width: 24px;
  height: 24px;
  cursor: pointer;
  background-image: url(~@/assets/copy.svg);
  background-repeat: no-repeat;
  background-size: 24px;
  position: absolute;
  left: -40px;
}
#converter .clear-btn {
}
#converter .copy-btn {
}
#converter .center {
  position: absolute;
  height: 100%;
  left: 50%;
  top: 0;
}
#converter .center-btn {
  height: 36px;
  width: 36px;
  border: 1px solid #e1e8ed;
  border-radius: 50%;
  background-image: url(~@/assets/switch-s.svg);
  background-repeat: no-repeat;
  background-position: 6px;
  background-size: 24px;
  position: absolute;
  left: -36px;
  top: 22px;
  /* animation: flip 250ms; */
}
#converter .center-line {
  background: linear-gradient(180deg, #e1e8ed, #f8fafc);
  position: absolute;
  top: 80px;
  height: calc(100% - 80px);
  width: 1px;
}
#converter .center-btn:hover {
  background-color: #eeeeee;
}
#converter .center-btn.flip {
  animation: flip 250ms;
}
.hover {
  position: relative;
}
.hover-text {
  transform: translateX(-50%);
  background-color: #4a4a4a;
  border-radius: 5px;
  line-height: 2;
  font-weight: 600;
  color: white;
  text-align: center;
  position: absolute;
  left: 50%;
  top: calc(100% + 10px);
  white-space: nowrap;
  padding: 0 8px;
  display: none;
}
.hover-text::before {
  content: "";
  display: inline-block;
  height: 0;
  width: 0;
  border-left: 6px solid transparent;
  border-right: 6px solid transparent;
  border-bottom: 6px solid #4a4a4a;
  transform: translateX(-50%);
  position: absolute;
  left: 50%;
  top: -6px;
}
.hover:hover .hover-text {
  display: block;
}
@keyframes flip {
  0% {
    transform-origin: center;
    transform: rotate3d(0, 0, 0, 0deg);
  }
  100% {
    transform-origin: center;
    transform: rotate3d(0, 0, 1, 180deg);
  }
}
</style>
<style>
.side:first-child textarea {
  padding-left: 0;
}
.side:last-child textarea {
  padding-right: 0;
}
</style>
