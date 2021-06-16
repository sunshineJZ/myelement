<template>
  <div class="container-myButton">
    <button
      ref="btn"
      :class="{ primary: primaryFlag, success: successFlag, info: infoFlag }"
      :disabled="disabled"
          >
      <i
        :class="{
          iconfont: true,
          'icon-container': true,
          'icon-jiazai1': iconFlag,
        }"
      ></i>
      <span v-show="showFlag">加载中</span>
      <span v-show="!showFlag">{{ value }}</span>
    </button>
  </div>
</template>

<script>
const classMap = {
  loading: "icon-jiazai1",
};
export default {
  data() {
    return {
      primaryFlag: false,
      successFlag: false,
      infoFlag: false,
      iconFlag: false,
      showFlag: false,
      domText: "",
    };
  },
  props: {
    type: {
      type: String,
      default: "primary",
    },
    loading: {
      type: Boolean,
      default: false,
    },
    value: {
      type: String,
    },
    disabled:{
      type:Boolean,
      default:false
    }
  },
  computed: {
    fontClass() {
      return classMap[this.type];
    },
  },
  created() {
    switch (this.type) {
      case "primary":
        this.primaryFlag = true;
        break;

      case "success":
        this.successFlag = true;
        break;
      case "info":
        this.infoFlag = true;
        break;
    }
  },
  mounted() {
    console.log(this.$refs.btn)
    this.domText = this.$refs.btn.innerText;
    if (this.loading) {
      this.showFlag = true;
      this.iconFlag = true;
    }
  },
};
</script>

<style scoped lang="less">
@import "//at.alicdn.com/t/font_2556020_sgxk7omx9db.css";

.container-myButton {
  width: 100px;
  height: 40px;
  button {
    display: flex;
    width: 100%;
    height: 100%;
    border-radius: 5px;
    color: #fff;
    border: 1px solid;
    cursor: pointer;
    align-items: center;
    justify-content: center;
    @keyframes move {
      0% {
        transform: rotateZ(0deg);
      }
      50% {
        transform: rotateZ(180deg);
      }
      100% {
        transform: rotateZ(360deg);
      }
    }
    &:disabled {
      cursor: not-allowed;
    }
    &.primary {
      background-color: #409eff;
      border-color: #409eff;
    }
    &.success {
      background-color: #67c23a;
      border-color: #67c23a;
    }
    &.info {
      background-color: #909399;
      border-color: #909399;
    }
    i {
      font-size: 26px;
      animation: move 2s infinite linear;
    }
  }
}
</style>