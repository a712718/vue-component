<template>
  <form class="el-form"
    :class="[
      labelPosition ? 'el-form--label-' + labelPosition : '',
      { 'el-form-inline': inline }
    ]"
  >
    <slot></slot>
  </form>
</template>
<script>
export default {
  name: 'ElFormMh',
  componentName: 'ElFormMh',
  props: {
    model: Object,
    rules: Object,
    labelPosition: String,
    labelWidth: String,
    inline: Boolean
  },
  data() {
    return {
      fields: [],
      potentialLabelWidthArr: []

    };
  },
  provide() {
    return {
      elForm: this
    };
  },
  created() {
    this.$on('el.form.addField', (field)=>{
      if (field) {
        this.fields.push(field);
      }
    });

    this.$on('el.form.removeField', (field) => {
      if (field.prop) {
        this.fields.splice(this.fields.indexOf(field), 1);
      }
    });
  },
  computed: {
    autoLabelWidth() {
      if (!this.potentialLabelWidthArr.length) return 0;
      const max = Math.max(...this.potentialLabelWidthArr);
      return max ? `${max}px` : '';
    }
  },
  methods: {
    getLabelWidthIndex(width) {
      const index = this.potentialLabelWidthArr.indexOf(width);
      if (index === -1) {
        throw new Error('[ElementForm] unexpect width', width);
      }
      return index;
    },
    registerLabelWidth(val, oldVal) {
      console.log('registerLabelWidth,,,,,', val, oldVal);
      if (val && oldVal) {
        const index = this.getLabelWidthIndex(oldVal);
        this.potentialLabelWidthArr.splice(index, 1, val);
      } else if (val) {
        this.potentialLabelWidthArr.push(val);
      }
    },
    removeLabelWidth(width) {
      const index = this.getLabelWidthIndex(width);
      this.potentialLabelWidthArr.splice(index, 1);
    }
  }
};
</script>
<style>

</style>