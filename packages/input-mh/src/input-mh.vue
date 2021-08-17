<template>
<div :class="[
  type==='textarea' ? 'el-textarea': 'el-input'
]">
  <template v-if="type!== 'textarea'">
    <!-- 前置元素 -->
    <div>
      <slot name="prepend"></slot>
    </div>
    <input
    ref="input"
    v-bind="$attrs"
    class="el-input__inner"
    @input="handleInput"
    @change="handleChange"/>
    <!-- 前置内容 -->
    <span>
    </span>
    <!-- 后置内容 -->
    <span class="el-input__suffix">
      <span v-if="isWordLimitVisible" class="el-input__count">
        <span class="el-input__count-inner">
          {{textLength}}/{{upperLimit}}
        </span>
      </span>
      <span v-if="!isWordLimitVisible">
        <slot name="suffix"></slot>
        <i v-if="suffixIcon" :class="suffixIcon" class="el-input__icon"></i>
      </span>
    </span>
    <!-- 后置元素 -->
    <div>
      <slot name="append"></slot>
    </div>
  </template>
  <template v-else>
    <textarea
    ref="textarea"
    v-bind="$attrs"
    class="el-textarea__inner"
    @input="handleInput"
    @change="handleChange"></textarea>
  </template>
</div>
</template>
<script>
  export default {
    name: 'ElInputMh',
    props: {
      value: [Number, String],
      type: {
        type: String,
        default: 'text'
      },
      suffixIcon: {
        type: String,
        default: ''
      }
    },
    computed: {
      nativeInputValue() {
        return this.value === undefined || this.value === null ? '' : String(this.value);
      },
      isWordLimitVisible() {
        return this.$attrs.maxlength;
      },
      upperLimit() {
        return this.$attrs.maxlength;
      },
      textLength() {
        return this.nativeInputValue.length;
      }
    },
    mounted() {
      this.setNativeInputValue();
      console.log('this.$attrs,,,,,', this.$attrs);
    },
    methods: {
      getInput() {
        return this.$refs.input || this.$refs.textarea;
      },
      setNativeInputValue() {
        const input = this.getInput();
        if (!input) return;
        if (input.value === this.nativeInputValue) return;
        input.value = this.nativeInputValue;
      },
      handleChange(event) {
        // event.target.value string类型
        this.$emit('change', event.target.value);
      },
      handleInput(event) {
        if (event.target.value === this.nativeInputValue) return;
        this.$emit('input', event.target.value);
      }
    }
  };
</script>
