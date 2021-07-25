<template>
  <div class="step-progress-box">
    <div class="step-progress" :style="{ width: width, height: height }">
      <div
        class="left-div-box"
        :style="{ width: stepsPercentUnit * activeStep + '%' }"
      >
        <div class="left-div"></div>
      </div>
      <div class="right-div"></div>
    </div>
    <div
      class="step-pointer"
      :style="{
        left:
          (100 * (activeStep || 0.01)) / (steps.length-1) -
          (activeStep ? 6 : 3) +
          '%',
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
};
</script>

<style lang="less">
.step-progress-box {
  position: relative;
  .step-progress-text-box {
    display: flex;
    justify-content: space-around;
  }
  .step-pointer {
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
    .left-div-box, .right-div{
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