<template>
  <button
  class="el-button"
  :type="nativeType"
  :disabled="disabled"
  :autofocus="autofocus"
  :class="[
  type ? 'el-button--' + type : '',
  size ? 'el-button--' + size: '', 
  { 'is-plain': plain,
    'is-round': round,
    'is-circle': circle,
    'is-loading': loading,
    'is-disabled': disabled
  }
  ]"
  @click="handleClick"
  >
  <i class="el-icon-loading" v-if="loading"></i>
  <i :class="icon" v-if="icon"></i>
  <slot></slot>
  </button>
</template>
<script>
  // (1)、type、size这种枚举类型的属性，样式名称用拼接的方式 el-button-primary, 这个样式里会有这个按钮所有状态（hover）的样式
  // (2)、plain、round、circle 这种 boolean类型的属性，用is-plain样式的添加与不添加
  // (3)、loading loading的样式+button中添加转圈圈图标
  // (4)、disabled disabled样式 + button原生disabled
  // (5)、click emit click
  export default {
    name: 'ElButtonMh',
    props: {
      size: {
        type: String,
        default: 'small'
      },
      type: {
        type: String,
        default: 'default'
      },
      plain: Boolean,
      round: Boolean,
      circle: Boolean,
      loading: Boolean,
      disabled: Boolean,
      autofocus: Boolean,
      icon: {
        type: String,
        default: ''
      },
      nativeType: {
        type: String,
        default: 'button'
      }
    },
    methods: {
      handleClick(event) {
        this.$emit('click', event);
      }
    }
  };
</script>