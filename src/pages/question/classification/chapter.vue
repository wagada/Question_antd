<template>
  <div id="Chapter">
    <a-Card :style="{'margin':'10px 0px'}">
    <!-- 行业和科目下拉框 -->
    <a-select
      show-search
      placeholder="行业"
      option-filter-prop="children"
      style="width: 200px"
      :filter-option="filterIndustry"
      @change="IndustryChange"
      :style="{'margin-right':'10px'}"
    >
      <a-select-option value="jack">互联网</a-select-option>
      <a-select-option value="lucy">电商</a-select-option>
      <a-select-option value="tom">服务业</a-select-option>
    </a-select>

    <a-select
      show-search
      placeholder="科目"
      option-filter-prop="children"
      style="width: 200px"
      :filter-option="filterSubject"
      @change="SubjectChange"
    >
      <a-select-option value="jack">语文</a-select-option>
      <a-select-option value="lucy">数学</a-select-option>
      <a-select-option value="tom">数学</a-select-option>
    </a-select>

    </a-Card>
    <a-card>
      <div class="buttonBox">
        <!-- <a-button @click="change" :style="{'margin-right':'10px'}" type="primary">添加行业</a-button>
        -->
        <!-- 添加章 -->
        <AddChapter />
        <a-button :style="{'background':'white','color':'red'}" type="danger">删除</a-button>
      </div>
      <a-table :columns="columns" :data-source="data" :row-selection="rowSelection">
        <template slot="operation" slot-scope="text, record">
          <div class="Flex">
            <a @click="EditModal" :style="{'margin-right':'10px'}" type="link">编辑</a>
            <!-- <a :style="{'color':'#63C83B'}" type="link">添加科目</a>
            -->
            <!-- 添加考点 -->
            <AddExamSite />
            <!-- 添加节 -->
            <AddSection />
          </div>
        </template>
      </a-table>
    </a-card>

    <a-modal
      title="编辑考点"
      :visible="EditVisible"
      :confirm-loading="confirmLoading"
      okText="保存"
      cancelText="删除"
      @ok="handleOk"
      @cancel="handleCancel"
    >
      <a-form
        :form="form"
        :label-col="{ span: 5 }"
        :wrapper-col="{ span: 11 }"
        @submit="handleSubmit"
      >
        <a-form-item label="行业">
          <!-- <a-input v-decorator="['name', { rules: [{ required: true, message: '请输选择所属!' }] }]" /> -->
          <a-select
            v-decorator="[
          'nameindustry',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
            placeholder="Select a option and change input text above"
          >
            <a-select-option value="male">male</a-select-option>
            <a-select-option value="female">female</a-select-option>
          </a-select>
        </a-form-item>

        <a-form-item label="科目">
          <!-- <a-input v-decorator="['name', { rules: [{ required: true, message: '请输选择所属!' }] }]" /> -->
          <a-select
            v-decorator="[
          'subject',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
            placeholder="Select a option and change input text above"
          >
            <a-select-option value="male">male</a-select-option>
            <a-select-option value="female">female</a-select-option>
          </a-select>
        </a-form-item>

        <a-form-item label="章">
          <!-- <a-input v-decorator="['name', { rules: [{ required: true, message: '请输选择所属!' }] }]" /> -->
          <a-select
            v-decorator="[
          'chapter',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
            placeholder="Select a option and change input text above"
          >
            <a-select-option value="male">male</a-select-option>
            <a-select-option value="female">female</a-select-option>
          </a-select>
        </a-form-item>

        <a-form-item label="节">
          <!-- <a-input v-decorator="['name', { rules: [{ required: true, message: '请输选择所属!' }] }]" /> -->
          <a-select
            v-decorator="[
          'section',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
            placeholder="Select a option and change input text above"
          >
            <a-select-option value="male">male</a-select-option>
            <a-select-option value="female">female</a-select-option>
          </a-select>
        </a-form-item>
        <a-form-item label="名称">
          <a-input v-decorator="['name', { rules: [{ required: true, message: '请输入名称!' }] }]" />
        </a-form-item>
        <a-form-item label="排序 考点">
          <a-input v-decorator="['name2', { rules: [{ required: true, message: '请输入考点!' }] }]" />
        </a-form-item>
      </a-form>
    </a-modal>
  </div>
</template>
<script>
const columns = [
  {
    title: '行业名称',
    dataIndex: 'name',
    key: 'name'
  },
  {
    title: '所属科目',
    dataIndex: 'age',
    key: 'age',
    width: '12%'
  },
  {
    title: '等级',
    dataIndex: 'level',
    // width: '30%',
    key: 'level'
  },
  {
    title: '排序',
    dataIndex: 'sort',
    // width: '30%',
    key: 'sort'
  },
  {
    title: '创建/修改时间',
    dataIndex: 'creatime',
    // width: '30%',
    key: 'creatime'
  },
  {
    title: '操作',
    dataIndex: 'operation',
    scopedSlots: { customRender: 'operation' }
  }
]

const data = [
  {
    key: 1,
    name: 'John Brown sr.',
    age: 60,
    address: 'New York No. 1 Lake Park',
    children: [
      {
        key: 11,
        name: 'John Brown',
        age: 42,
        address: 'New York No. 2 Lake Park'
      },
      {
        key: 12,
        name: 'John Brown jr.',
        age: 30,
        address: 'New York No. 3 Lake Park',
        children: [
          {
            key: 121,
            name: 'Jimmy Brown',
            age: 16,
            address: 'New York No. 3 Lake Park'
          }
        ]
      },
      {
        key: 13,
        name: 'Jim Green sr.',
        age: 72,
        address: 'London No. 1 Lake Park',
        children: [
          {
            key: 131,
            name: 'Jim Green',
            age: 42,
            address: 'London No. 2 Lake Park',
            children: [
              {
                key: 1311,
                name: 'Jim Green jr.',
                age: 25,
                address: 'London No. 3 Lake Park'
              },
              {
                key: 1312,
                name: 'Jimmy Green sr.',
                age: 18,
                address: 'London No. 4 Lake Park'
              }
            ]
          }
        ]
      }
    ]
  },
  {
    key: 2,
    name: 'Joe Black',
    age: 32,
    address: 'Sidney No. 1 Lake Park'
  }
]

const rowSelection = {
  onChange: (selectedRowKeys, selectedRows) => {
    console.log(`selectedRowKeys: ${selectedRowKeys}`, 'selectedRows: ', selectedRows)
  },
  onSelect: (record, selected, selectedRows) => {
    console.log(record, selected, selectedRows)
  },
  onSelectAll: (selected, selectedRows, changeRows) => {
    console.log(selected, selectedRows, changeRows)
  }
}
import AddExamSite from './components/AddExamSite'
import AddChapter from './components/AddChapter'
import AddSection from './components/AddSection'
export default {
  data() {
    return {
      data,
      columns,
      rowSelection,
      AddIndustryVisible: false,
      AddsubjectVisible: false,
      // 编辑
      form: this.$form.createForm(this, { name: 'coordinated' }),
      EditVisible: false,
      confirmLoading: false
    }
  },
  methods: {
    // 编辑
    EditModal() {
      this.EditVisible = true
    },
    handleSubmit(e) {
      e.preventDefault()
      this.confirmLoading = true
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values)
          return err
        } else {
          this.EditVisible = false
          this.confirmLoading = false
        }
      })
    },
    handleOk(e) {
      this.confirmLoading = true
      setTimeout(() => {
        this.EditVisible = false
        this.confirmLoading = false
      }, 2000)
    },
    handleCancel(e) {
      console.log('Clicked cancel button')
      this.EditVisible = false
    },
    // 行业下拉框改变
    IndustryChange(value) {
      console.log(`selected ${value}`)
    },
    filterIndustry(input, option) {
      return option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0
    },
    // 科目下拉框
    SubjectChange(value) {
      console.log(`selected ${value}`)
    },
    filterSubject(input, option){
        return option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0
    }
  },
  components: {
    AddExamSite,
    AddChapter,
    AddSection
  }
}
</script>
<style >
#Chapter .buttonBox {
  margin-bottom: 10px;
  display: flex;
}
#Chapter .ant-table-thead > tr > th {
  color: white;
  background: #4a90e2 !important;
}
.Flex {
  display: flex;
}
</style>
