<template>
  <div class="app-container">
    <query-form :fields="fields" />
  </div>
</template>

<script>
import QueryForm from '@/components/QueryForm'

import cities from '@/utils/cities.json'
const fields = [
  {
    tag: 'el-input',
    label: '企业名称',
    name: 'companyName',
    placeholder: '请输入企业名称',
    rules: []
  },
  {
    tag: 'el-cascader',
    label: '地区',
    name: 'area',
    placeholder: '请选择地区',
    options: cities,
    props: {
      props: {
        value: 'code',
        label: 'name'
      }
    }
  },
  {
    tag: 'el-select',
    label: '行业',
    name: 'industry',
    placeholder: '请选择行业',
    rules: [],

    __slot__: {
      options: [
        { label: '种植', value: '1' },
        { label: '餐饮', value: '2' }
      ]
    }
  },
  {
    tag: 'el-select',
    label: '企业类型',
    name: 'companyType',
    placeholder: '请选择企业类型',
    rules: [],
    options: [
      { label: '个人', value: '1' },
      { label: '集体', value: '2' }
    ]
  },
  {
    tag: 'el-select',
    label: '注册资本',
    name: 'registeredCapital',
    placeholder: '请选择注册资本',
    rules: [],
    options: [
      { label: '小于10万', value: '1' },
      { label: '10-100万', value: '2' },
      { label: '大于10-100万', value: '2' }
    ]
  },
  {
    tag: 'el-select',
    label: '实缴资本',
    name: 'contributedCapital',
    placeholder: '请选择实缴资本',
    rules: [],
    options: [
      { label: '小于10万', value: '1' },
      { label: '大于100万', value: '2' }
    ]
  },
  {
    tag: 'el-date-picker',
    label: '成立年份',
    name: 'registeredYear',
    placeholder: '请选择成立年份',
    rules: [],
    props: { type: 'year' }
  },
  {
    tag: 'el-date-picker',
    label: '结束年份',
    name: 'endYear',
    placeholder: '请选择结束年份',
    rules: [],
    props: { type: 'year' }
  },
  {
    tag: 'el-select',
    label: '客户标签',
    name: 'tag',
    placeholder: '请选择客户标签',
    rules: [],
    options: [
      { label: '标签1', value: '1' },
      { label: '标签2', value: '2' }
    ]
  },
  {
    tag: 'el-select',
    label: '客户状态',
    name: 'status',
    placeholder: '请选择客户状态',
    rules: [],
    options: [
      { label: '状态1', value: '1' },
      { label: '状态2', value: '2' }
    ]
  },
  {
    tag: 'el-select',
    label: '客户意向',
    name: 'intention',
    placeholder: '请选择客户意向',
    rules: [],
    options: [
      { label: '意向1', value: '1' },
      { label: '意向2', value: '2' }
    ]
  },
  {
    tag: 'el-select',
    label: '归属人',
    name: 'belonger',
    placeholder: '请选择归属人',
    rules: [],
    options: [
      { label: 'A', value: '1' },
      { label: 'B', value: '2' }
    ]
  },
  {
    tag: 'el-select',
    label: '创建人',
    name: 'creator',
    placeholder: '请选择创建人',
    rules: [],
    options: [
      { label: 'A', value: '1' },
      { label: 'B', value: '2' }
    ]
  }
]

export default {
  components: {
    QueryForm
  },

  data() {
    return {
      fields
    }
  },

  methods: {
    onSwitch() {
      this.isOpen = !this.isOpen
    }
  }
}
</script>

<style lang="scss" scoped>
.col {
  height: 40px;
  background-color: #ff0;
  margin-bottom: 12px;
}
</style>
