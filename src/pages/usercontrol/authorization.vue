<template>
  <div id="authorization">
    <a-Card :style="{'border-radius':'6px'}">
      <div :style="{'margin':'25px','display':'flex'}" class="info">
          <!-- 头像 -->
        <div class="avatars"></div>
        <!-- 网校信息 -->
        <div class="userinfo">
          <p>
            昵称
            <span>维他柠檬茶</span>
          </p>
          <p>
            手机号
            <span>111111111111</span>
          </p>
          <p>
            备注
            <span>你爹我</span>
          </p>
        </div>
      </div>
      <h1>已有授权</h1>
      <a-table :columns="columns" :data-source="data">
        <template slot="operation" slot-scope="text, record">
          <a @click="showConfirm(record)" type="link">取消授权</a>
        </template>
        <!-- 授权信息表单 -->
        <template v-if="addper" class="footer" slot="footer" slot-scope="currentPageData">
          <a-form
            :style="{'display':'flex','align-item':'center'}"
            :form="form"
            :label-col="{ span: 5 }"
            :wrapper-col="{ span: 12 }"
            @submit="handleSubmit"
          >
            <a-form-item label>
              <a-select
                v-decorator="[
            'schoolname',
            {rules: [{ required: true, }]}
          ]"
                show-search
                placeholder="搜索网校"
                style="width: 120px"
              >
                <a-select-option value="职考通关">职考通关</a-select-option>
                <a-select-option value="短书">短书</a-select-option>
                <a-select-option value="哇嘎达">哇嘎达</a-select-option>
              </a-select>
            </a-form-item>
            <a-form-item label>
              <a-select
                show-search
                placeholder="行业"
                option-filter-prop="children"
                style="width: 120px"
                :filter-option="filterIndustry"
                v-decorator="[
          'industry',
          { rules: [{ required: true, message: '请选择行业!' }] },
        ]"
              >
                <a-select-option value="互联网">互联网</a-select-option>
                <a-select-option value="教育">教育</a-select-option>
                <a-select-option value="服务">服务</a-select-option>
              </a-select>
            </a-form-item>
            <a-form-item label>
              <a-select
                show-search
                placeholder="科目"
                option-filter-prop="children"
                style="width: 120px"
                :filter-option="filterSubject"
                v-decorator="[
          'subject',
          { rules: [{ required: true, message: '请选择科目!' }] },
        ]"
              >
                <a-select-option value="项目管理">项目管理</a-select-option>
                <a-select-option value="系统集成">系统集成</a-select-option>
                <a-select-option value="中学教资">中学教资</a-select-option>
              </a-select>
            </a-form-item>
            <div :style="{'margin-top':'4px'}">
              <a-button class="bluefont" @click="handleSubmit">确认</a-button>
              <a-button @click="changeAddper">取消</a-button>
            </div>
          </a-form>
        </template>
      </a-table>
      <a v-if="!addper" @click="changeAddper" :style="{'position':'absolute','bottom':'60px','font-weight':'400'}">添加授权</a>
    </a-Card>
    
  </div>
</template>

<script>
const columns = [
  {
    title: '来源网校',
    dataIndex: 'name',
    key: 'name'
  },
  {
    title: '授权行业',
    dataIndex: 'age',
    key: 'age'
  },
  {
    title: '授权科目',
    dataIndex: 'address',
    key: 'address'
  },
  {
    title: '授权时间',
    dataIndex: 'creatime',
    key: 'creatime'
  },
  {
    title: 'Opction',
    key: 'Opction',
    scopedSlots: { customRender: 'operation' }
  }
]

const data = [
  {
    key: 1,
    name: 'John Brown sr.',
    age: 60,
    address: 'New York No. 1 Lake Park'
  },
  {
    key: 2,
    name: 'Joe Black',
    age: 32,
    address: 'Sidney No. 1 Lake Park'
  }
]

export default {
  data() {
    return {
      data,
      columns,
      form: this.$form.createForm(this, { name: 'coordinated' }),
        // 添加授权时出现对应表单和隐藏添加授权
      addper:false
    }
  },
  methods: {
    //   可搜索下拉框 ——选择网校搜索子项
    filterSchoolname(input, option) {
      return option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0
    },
    //   可搜索下拉框 ——选择行业搜索子项
    filterIndustry(input, option) {
      return option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0
    },
    //   可搜索下拉框 ——选择科目搜索子项
    filterSubject(input, option) {
      return option.componentOptions.children[0].text.toLowerCase().indexOf(input.toLowerCase()) >= 0
    },
    //  提交表单
    handleSubmit(e) {
      e.preventDefault()
      this.form.validateFields((err, values) => {
        if (err) {
          console.log('Received values of form: ', values)
          this.$message.error('This is an error message')
        } else {
          console.log(values)
        }
      })
    },
    // 点击添加授权
    changeAddper(){
        this.addper = !this.addper
    },
    // 取消授权
    showConfirm(record) {
        console.log(record)
      this.$confirm({
        content: h => <div>
            <p style="color:#666666;text-align:center,"> 确认取消授权？</p>
            <div style="display:flex;justify-content:space-around;color:#333333;">
                <span>昵称</span>
                <span>手机号</span>
                <span>行业</span>
                <span>科目</span>
            </div>
            <div style="display:flex;justify-content:space-around;color:#333333;">
                <span>昵称</span>
                <span>手机号</span>
                <span>行业</span>
                <span>科目</span>
            </div>
        </div>,
        okText: '确认',
        cancelText: '取消',
        onOk() {
          console.log('OK');
        },
        onCancel() {
          console.log('Cancel');
        },
        class: 'test',
      });
    },
  }
}
</script>
<style >
#authorization p {
  margin: 0px;
  font-family: Microsoft YaHei;
  font-weight: bold;
}
#authorization h1 {
  width: 74px;
  height: 24px;
  font-size: 18px;
  font-family: Microsoft YaHei;
  font-weight: 400;
  line-height: 24px;
  color: rgba(51, 51, 51, 1);
  opacity: 1;
}
#authorization p span {
  margin-left: 10px;
  font-weight: 500;
}
#authorization .info {
  height: 100px;
}
#authorization .avatars {
  width: 100px;
  height: 100px;
  border: 1px solid #000;
  justify-content: flex-start;
  margin-right: 25px;
}
#authorization .userinfo {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
#authorization td {
  text-align: center !important;
}
#authorization th {
  text-align: center !important;
}
#authorization .ant-table-thead > tr > th {
  color: white;
  background: #1990ff !important;
}
#authorization .ant-table {
  border-left: 1px solid #dcdcdc;
  border-right: 1px solid #dcdcdc;
  border-bottom: 1px solid #dcdcdc;
  border-radius: 4px;
}
#authorization .ant-table-footer {
  background-color: white;
  margin-left: 50px;
}
#authorization .ant-form .ant-form-item {
  margin-bottom: 0px;
  margin-right: 69px;
}
#authorization .ant-form {
  display: flex;
  align-content: center;
}
#authorization .bluefont {
  border: 1px solid #1990ff;
  color: #1990ff;
  margin-right: 10px;
}
.ant-modal-body .ant-modal-confirm-btns{
    float: none;
    display: flex;
    justify-content: center;
}
</style>