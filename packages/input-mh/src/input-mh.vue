<template>
<div>
  <template v-if="type!== 'textarea'">
    <input
    ref="input"
    @input="handleInput"
    @change="handleChange"/>
  </template>
  <template v-else>
    <textarea
    ref="textarea"
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
      }
    },
    computed: {
      nativeInputValue() {
        return this.value === undefined || this.value === null ? '' : String(this.value);
      }
    },
    mounted() {
      this.setNativeInputValue();
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
