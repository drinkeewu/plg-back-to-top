<template>
  <div
    :style="styles"
    :class="classes"
    @click="onBack"
  >
    <slot>
      <i class="iconfont icon-arrowup" />
    </slot>
  </div>
</template>

<script>
import { on, off } from '../../../utils/dom';
import { scrollTop } from '../../../utils/assist';

const prefixCls = 'dr-back-top';
export default {
  name: 'BackToTop',
  props: {
    height: {
      type: Number,
      default: 200,
    },
    bottom: {
      type: Number,
      default: 150,
    },
    right: {
      type: Number,
      default: 100,
    },
    duration: {
      type: Number,
      default: 1000,
    },
  },
  data() {
    return {
      backTop: false,
    };
  },
  computed: {
    styles() {
      return {
        bottom: `${this.bottom}px`,
        right: `${this.right}px`,
      };
    },
    classes() {
      return [
        `${prefixCls}`,
        {
          [`${prefixCls}-show`]: this.backTop,
        },
      ];
    },
  },
  mounted() {
    on(window, 'scroll', this.handleScroll);
    on(window, 'resize', this.handleScroll);
  },
  beforeDestroy() {
    off(window, 'scroll', this.handleScroll);
    off(window, 'resize', this.handleScroll);
  },
  methods: {
    onBack() {
      const sTop = document.documentElement.scrollTop || document.body.scrollTop;
      scrollTop(window, sTop, 0, this.duration);
      this.$emit('on-click');
    },
    handleScroll() {
      this.backTop = window.pageYOffset >= this.height;
    },
  },
};
</script>

<style lang="scss" scoped>
@import url("./icon/iconfont.css");
.dr-back-top {
  display: none;
  background-color: #fff;
  position: fixed;
  width: 40px;
  height: 40px;
  border-radius: 20px;
  cursor: pointer;
  transition: 0.3s;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.12);
  z-index: 5;
  justify-content: center;
  align-items: center;
  &.dr-back-top-show {
    display: flex;
  }
  .icon-arrowup {
    color: #909399;
    display: block;
    line-height: 40px;
    text-align: center;
    font-size: 30px;
  }
}
</style>
