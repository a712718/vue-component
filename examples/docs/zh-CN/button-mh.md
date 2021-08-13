## Button MH 按钮

### 基础用法

:::demo

```html
<el-row>
  <el-button-mh>默认按钮</el-button-mh>
  <el-button-mh type="primary">主要按钮</el-button-mh>
  <el-button-mh type="primary" :plain="true">plain</el-button-mh>
  <el-button-mh type="primary" :round="true">round</el-button-mh>
  <el-button-mh type="primary" :circle="true">circle</el-button-mh>
  <el-button-mh type="primary" :loading="true">loading</el-button-mh>
  <el-button-mh type="primary" disabled>disabled</el-button-mh>
  <el-button-mh type="primary" @click="handleClick">click</el-button-mh>
  <el-button-mh type="primary" icon="el-icon-edit">icon</el-button-mh>
  <el-button-mh type="primary" native-type="submit">submit</el-button-mh>
</el-row>

<el-row>
  <el-button-mh type="primary" autofocus>autofocus</el-button-mh>
</el-row>

<script>
  export default {
    data() {
      return {}
    },
    methods: {
      handleClick() {
        alert('click button');
      }
    }
  }
</script>
```
:::

### button-group

:::demo

```html
  <el-button-group-mh>
    <el-button-mh>默认按钮</el-button-mh>
    <el-button-mh type="primary">主要按钮</el-button-mh>
  </el-button-group-mh>
```
:::