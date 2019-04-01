<template>
  <div
    ref="backToTop"
    class="dr-back-to-top"
    :style="wrapperStyle"
    @click.stop="onClick"
  >
    <slot>
      <i class="iconfont icon-arrowup" />
    </slot>
  </div>
</template>

<script>
export default {
  name: 'BackToTop',
  props: {
    height: {
      type: Number,
      default: 200,
    },
    customStyle: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      el: null,
    };
  },
  computed: {
    wrapperStyle() {
      return this.customStyle;
    },
  },
  mounted() {
    this.initElement();
    this.addScrollListener();
  },
  methods: {
    addScrollListener() {
      window.addEventListener('scroll', this.onScroll, false);
    },
    showCaret() {
      this.el.style.display = 'flex';
    },
    hideCaret() {
      this.el.style.display = 'none';
    },
    initElement() {
      this.el = this.$refs.backToTop;
    },
    onScroll() {
      const scrollTop = document.body.scrollTop
        || document.documentElement.scrollTop
        || 0;
      if (scrollTop > this.height) {
        this.showCaret();
      } else {
        this.hideCaret();
      }
    },
    onClick() {
      window.scroll(0, 0);
    },
  },
};
</script>

<style lang="scss" scoped>
@import url('./icon/iconfont.css');
.dr-back-to-top {
  display: none;
  background-color: #fff;
  position: fixed;
  right: 100px;
  bottom: 150px;
  width: 40px;
  height: 40px;
  border-radius: 20px;
  cursor: pointer;
  transition: 0.3s;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.12);
  z-index: 5;
  display: flex;
  justify-content: center;
  align-items: center;
  .icon-arrowup{
    color: #909399;
    display: block;
    line-height: 40px;
    text-align: center;
    font-size: 30px;
  }
}
</style>
