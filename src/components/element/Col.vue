<template>
  <div :class="[`el-col `, ...classList]" :style="style">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    span: {
      type: Number,
      default: 24,
    },
    offset: {
      type: Number,
      default: 0,
    },
    push: {
      type: Number,
      default: 0,
    },
    pull: {
      type: Number,
      default: 0,
    },
    xs: {
      type: [Number, Object],
    },
    sm: {
      type: [Number, Object],
    },
    md: {
      type: [Number, Object],
    },
    lg: {
      type: [Number, Object],
    },
    xl: {
      type: [Number, Object],
    },
  },
  computed: {
    gutter() {
      let parent = this.$parent;
      while (parent && parent.$options.name != "ElRow") {
        parent = parent.$parent;
      }
      return parent ? parent.gutter : 0;
    },
    style() {
      const style = {};
      if (this.gutter) {
        style.paddingLeft = this.gutter / 2 + "px";
        style.paddingRight = this.gutter / 2 + "px";
      }
      return style;
    },

    classList() {
      const list = [];
      ["span", "offset", "push", "pull"].forEach((ele) => {
        if (this[ele]) {
          list.push(
            ele == "span" ? `el-col-${this[ele]}` : `el-col-${ele}-${this[ele]}`
          );
        }
      });
      ["xs", "sm", "md", "lg", "xl"].forEach((ele) => {
        if (typeof this[ele] == "number") {
          list.push(`el-col-${ele}-${this[ele]}`);
        } else if (typeof this[ele] == "object") {
          for (var prop in this[ele]) {
            if (prop == "span") {
              list.push(`el-col-${prop}-${this[ele][prop]}`);
            } else {
              list.push(`el-col-${prop}-${this[ele][prop]}`);
            }
          }
        }
      });
      console.log(list);
      return list;
    },
  },
};
</script>

<style lang="less" scoped>
.el-col {
  float: left;
  box-sizing: border-box;
}

.loopWidth(@i) when ( @i < 25) {
  .el-col-@{i} {
    width: @i / 24 * 100%;
  }
  .el-col-offset-@{i} {
    margin-left: @i / 24 * 100%;
  }
  .el-col-push-@{i} {
    position: relative;
    left: @i / 24 * 100%;
  }

  .el-col-pull-@{i} {
    position: relative;
    right: @i / 24 * 100%;
  }

  .el-col-xs-@{i} {
    @media screen and (max-width: 720px) {
      width: @i / 24 * 720;
    }
  }
    .el-col-sm-@{i} {
    @media screen and (max-width: 720px) {
      width: @i / 24 * 720;
    }
  }
    .el-col-md-@{i} {
    @media screen and (max-width: 720px) {
      width: @i / 24 * 720;
    }
  }
    .el-col-lg-@{i} {
    @media screen and (max-width: 720px) {
      width: @i / 24 * 720;
    }
  }
    .el-col-xl-@{i} {
    @media screen and (max-width: 720px) {
      width: @i / 24 * 720;
    }
  }

  .loopWidth(@i + 1);
}

.loopWidth(1);
</style>