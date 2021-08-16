## InputMh 输入框
通过鼠标或者键盘输入字符

:::warning
Input为受控组件
:::

### 基础用法

这个组件字符串

:::demo
```html
<el-input-mh v-model="value" placeholder="请输入内容" @change="handleChange"/>
<script>
  export default {
    data () {
      return {
        value: 123
      }
    },
    updated() {
      console.log('value,,,,,,,,,', this.value);
    },
    methods: {
      handleChange(value) {
        console.log('md handleChange value', value);
        console.log('md this.value', this.value);
      }
    }
  }
</script>
```
:::

### textarea

:::demo
```html
<el-input-mh v-model="value" type="textarea" placeholder="请输入内容" />
<script>
  export default {
    data () {
      return {
        value: 123
      }
    },
    updated() {
      console.log('value,,,,,,,,,', this.value);
    }
  }
</script>
```
:::