<script>
export default {
  props: {
    isAutoWidth: Boolean,
    updateAll: Boolean
  },
  inject: ['elForm', 'elFormItem'],
  render() {
    const slots = this.$slots.default;
    console.log('slots,,,,,', slots);
    console.log('this.isAutoWidth,,,,', this.isAutoWidth);
    if (!slots) return null;
    if (this.isAutoWidth) {
      const autoLabelWidth = this.elForm.autoLabelWidth;
      const style = {};
      if (autoLabelWidth && autoLabelWidth !== 'auto') {
        const marginLeft = parseInt(autoLabelWidth, 10) - this.computedWidth;
        style.marginLeft = marginLeft;
      }
      return (<div class="el-form-item__label-wrap" style={style}>{slots}</div>);
    } else {
      return slots[0];
    }
  },
  methods: {
    getLabelWidth() {
      if (this.$el && this.$el.firstElementChild) {
        const computedWidth = window.getComputedStyle(this.$el.firstElementChild).width;
        return Math.ceil(parseFloat(computedWidth));
      } else {
        return 0;
      }
    },
    updateLabelWidth(action = 'update') {
      if (this.$slots.default && this.isAutoWidth && this.$el.firstElementChild) {
        if (action === 'update') {
          this.computedWidth = this.getLabelWidth();
        } else if (action === 'remove') {
          this.elForm.deregisterLabelWidth(this.computedWidth);
        }
      }
    }
  },
  watch: {
    computedWidth(val, oldVal) {
      if (this.updateAll) {
        this.elForm.registerLabelWidth(val, oldVal);
        this.elFormItem.updateComputedLabelWidth();
      }
    }
  },
  data() {
    return {
      computedWidth: 0
    };
  },
  mounted() {
    // 每创建一个form-item就会计算label的宽度computedWidth
    // computedWidth 检测computedWidth的变化去调用 this.elForm.registerLabelWidth(val, oldVal);
    // 改变 potentialLabelWidthArr， 根据potentialLabelWidthArr变化，从中间取得最大的label的宽度
    this.updateLabelWidth('update');
  },
  updated() {
    this.updateLabelWidth('update');
  },
  beforeDestroy() {
    this.updateLabelWidth('remove');
  }
};
</script>

<style scoped>
</style>