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

### size

:::demo
```html
<el-input-mh v-model="value" placeholder="mini" size="mini"/>
<el-input-mh v-model="value" placeholder="small" size="small"/>
<el-input-mh v-model="value" placeholder="medium" size="medium"/>
<el-input-mh v-model="value" placeholder="large" size="large"/>
<el-input-mh v-model="value" placeholder="请输入内容"/>
<script>
  export default {
    data () {
      return {
        value: ''
      }
    },
  }
</script>
```
:::
### maxlength/minlength


:::demo
```html
<el-input-mh v-model="value" placeholder="请输入内容" :maxlength="10"/>
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

### 带icon的输入框


:::demo
```html
<el-input-mh
  v-model="value"
  placeholder="请输入内容"
  suffix-icon="el-icon-search"
  />
<el-input-mh
  v-model="value"
  placeholder="请输入内容"
  >
  <i slot="suffix" class="el-input__icon el-icon-date"></i>
</el-input-mh>
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

### 复合型输入框

:::demo
```html
<el-input-mh
  v-model="value"
  placeholder="请输入内容"
  >
  <template slot="prepend">http://</template>
</el-input-mh>
<el-input-mh
  v-model="value"
  placeholder="请输入内容"
  >
   <template slot="append"><i class="el-input__icon el-icon-date"></i></template>
  
</el-input-mh>
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