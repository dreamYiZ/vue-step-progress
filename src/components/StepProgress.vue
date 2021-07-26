<template>
  <div class="step-progress-box" @click="stepOnClick">
    <div class="step-progress" :style="{ width: width, height: height }">
      <div class="left-div click-event"></div>
      <div
        class="right-div click-event"
        :style="{ width: 100 - stepsPercentUnit * activeStep + '%' }"
      ></div>
    </div>
    <div
      class="step-pointer"
      :class="{'step-first': activeStep===0, 'step-last': activeStep===(steps.length-1)}"
      :style="{
        left: (100 * (activeStep || 0.01)) / (steps.length - 1)  + '%',
      }"
    >
      <div
        class="step-pointer-inner"
        :style="{ background: pointerBgColorArr[activeStep] }"
      ></div>
    </div>
    <div class="step-progress-text-box">
      <div class="step-label" v-for="(step, idx) in steps" :key="idx">
        {{ step }}
      </div>
    </div>
  </div>
</template>


<script>
import RLog from "rentoo";

export default {
  props: {
    width: {
      type: String,
      default: "100%",
    },
    height: {
      type: String,
      default: "20px",
    },
    activeStep: {
      type: Number,
      default: 0,
    },
    steps: {
      type: Array,
      default: function () {
        return [1, 2, 3, 4];
      },
    },
  },
  data() {
    return {
      pointerBgColorArr: [
        "rgba(248, 236, 92, 1)",
        "rgba(254, 194, 72, 1)",
        "rgba(246, 103, 73, 1)",
        "rgba(231, 33, 4, 1)",
      ],
    };
  },
  computed: {
    stepsPercentUnit: function () {
      return 100 / (this.steps.length - 1);
    },
  },
  methods: {
    stepOnClick(e) {
      if (!e.target.classList.contains("click-event")) {
        return;
      }
      RLog(
        e,
        e.clientX,
        e.target.clientWidth,
        e.clientX / e.target.clientWidth
      );
      let twidth = e.target.clientWidth;
      let ex = e.clientX;
      let deviation = twidth / 20;
      if (ex < twidth / 4 + deviation) {
        RLog("emit" + 0);
        this.$emit("change", 0);
        return;
      }

      if (ex > twidth / 4 + deviation && ex < (twidth / 4) * 2 - deviation) {
        RLog("emit" + 1);
        this.$emit("change", 1);
        return;
      }

      if (
        ex > (twidth / 4) * 2 + deviation &&
        ex < (twidth / 4) * 3 + 10 * deviation
      ) {
        RLog("emit" + 2);
        this.$emit("change", 2);
        return;
      }

      if (ex > (twidth / 4) * 3 + 16 * deviation) {
        RLog("emit" + 3);
        this.$emit("change", 3);
        return;
      }
    },
  },
};
</script>

<style lang="less">
.step-progress-box {
  position: relative;
  overflow: hidden;
  .step-progress-text-box {
    display: flex;
    justify-content: space-between;
  }
  .step-pointer {
    transform: translateX(-50%);
    position: absolute;
    top: 0;
    z-index: 99;
    width: 34px;
    height: 34px;
    display: flex;
    align-items: center;
    justify-content: center;
    // box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    // border: 6px solid #FFF;
    // box-shadow: 0px 0px 0px 10px blue;
    border-radius: 50%;
    // background-color: #000;
    background-color: rgba(255, 255, 255, 0.5);
    &.step-first{
      transform: translateX(-30%);
    }
    &.step-last{
      transform: translateX(-100%);
    }
    .step-pointer-inner {
      width: 24px;
      border-radius: 50%;
      height: 24px;
      background-color: #000;
    }
  }
  .step-progress {
    position: relative;
    height: 20px;
    width: 100%;
    border-radius: 100px;
    overflow: hidden;
    top: 8px;
    .left-div-box {
      z-index: 50;
      left: 0;
    }
    .left-div-box,
    .right-div {
      position: absolute;
      top: 0;
    }
    .left-div,
    .right-div {
      width: 100%;
      height: 20px;
    }
    .left-div {
      background-color: red;
      background: rgb(248, 236, 92);
      background: linear-gradient(
        90deg,
        rgba(248, 236, 92, 1) 0%,
        rgba(254, 194, 72, 1) 25%,
        rgba(246, 103, 73, 1) 69%,
        rgba(231, 33, 4, 1) 100%
      );
    }
    .right-div {
      right: 0;
      z-index: 30;
      background: rgb(49, 166, 113);
    }
  }
  .step-progress-text-box {
    margin-top: 8px;
  }
}
</style>