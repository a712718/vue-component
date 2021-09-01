## Form Mh 表单

由输入框、选择器、单选框、多选框等控件组成，用于收集、校验、提交数据

#### 典型表单

::: demo 
```html
<el-form-mh :model="form">
  <el-form-item-mh label="名称">
    <el-input v-model="form.name" />
  </el-form-item-mh>
  <el-form-item-mh label="名称">
    <el-input v-model="form.age" />
  </el-form-item-mh>
</el-form-mh>
<script>
  export default {
    data () {
      return {
        form: {
          name: 'mahong',
          age: 18
        }
      }
    }
  }
</script>
```

