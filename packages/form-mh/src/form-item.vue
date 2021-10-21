<template>
  <div class="el-form-item__content">
    <label-wrap
    :is-auto-width="labelStyle && labelStyle.width === 'auto'"
    :update-all="form.labelWidth === 'auto'"
    >
      <label class="el-form-item__label" style="labelStyle">{{ label }}</label>
    </label-wrap>
    <div class="el-form-item__content" :style="contentStyle">
      <slot></slot>
    </div>
  </div>
</template>
<script>
import labelWrap from './label-wrap.vue';
export default {
  props: {
    label: String,
    labelWidth: String
  },
  name: 'ElFormItemMh',
  componentName: 'ElFormItemMh',
  components: {
    labelWrap
  },
  inject: ['elForm'],
  data() {
    return {
      isNested: false,
      computedLabelWidth: ''
    };
  },
  computed: {
    labelStyle() {
      const ret = {};
      console.log('this.form,,,,,,,', this.form);
      if (this.form.labelPosition === 'top') return ret;
      console.log('this.labelWidth,,,,,', this.labelWidth);
      console.log('this.form.labelWidth,,,,,', this.form.labelWidth);
      const labelWidth = this.labelWidth || this.form.labelWidth;
      if (labelWidth) {
        ret.width = labelWidth;
      }
      console.log('labelStyle,,,,,', ret);
      return ret;
    },
    // 取form
    form() {
      let parent = this.$parent;
      let parentName = parent.$options.componentName;
      while (parentName !== 'ElFormMh') {
        if (parentName === 'ElFormItemMh') {
          this.isNested = true;
        }
        parent = parent.$parent;
        parentName = parent.$options.componentName;
      }
      return parent;
    },
    contentStyle() {
      const ret = {};
      const label = this.label;
      if (this.form.labelPosition === 'top' || this.form.inline) return ret;
      if (!label && !this.labelWidth && this.isNested) return ret;
      const labelWidth = this.labelWidth || this.form.labelWidth;
      if (labelWidth === 'auto') {
        if (this.labelWidth === 'auto') {
          ret.marginLeft = this.computedLabelWidth;
        } else if (this.form.labelWidth === 'auto') {
          // form label-width = 'auto'
          console.log('this.elForm.autoLabelWidth,,,,,', this.elForm.autoLabelWidth);
          ret.marginLeft = this.elForm.autoLabelWidth;
        }
      } else {
        ret.marginLeft = this.elForm.labelWidth;
      }
      console.log('contentStyle ret,,,,,,', ret);
      return ret;
    }
  },
  provide() {
    return {
      elFormItem: this
    };
  },
  created() {
  },
  methods: {
    updateComputedLabelWidth(width) {
      this.computedLabelWidth = width ? `${width}px` : '';
    }
  }
};
</script>
<style>

</style>