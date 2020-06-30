<template>
  <div id="Accountsettings">
    <!-- 添加帐号和搜索 -->
    <a-Card :style="{'border-radius':'6px','margin-bottom':'10px'}">
      <div :style="{'display':'flex','justify-content':'space-between'}">
        <a-button @click="showModal" :style="{'border-radius':'4px'}" type="primary">添加帐号</a-button>
        <a-input-search
          :style="{'width':'200px',}"
          placeholder="input search text"
          enter-button
          @search="onSearch"
        />
      </div>
    </a-Card>
    <!-- 帐号表格 -->
    <a-Card>
      <a-table :columns="columns" :data-source="data">
        <template slot="opction" slot-scope="opction">
          <div :style="{'display':'flex','justify-content':'space-around'}">
            <a :style="{'color':'#1990FF'}">编辑</a>
            <a :style="{'color':'#FF5757'}">删除</a>
          </div>
        </template>
      </a-table>
    </a-Card>

    <!-- 添加帐号弹窗表单 -->
    <a-modal v-model="Addaccount" title="账号添加" @ok="handleOk">
      <a-form :form="form" @submit="handleSubmit">
        <a-form-item
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
          label="帐号"
        >
          <a-input
            v-decorator="[
          'account',
          { rules: [{ required: true, message: '请输入帐号' }] },
        ]"
          />
        </a-form-item>
        <a-form-item
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
          label="姓名"
        >
          <a-input v-decorator="['name',]" placeholder="输入您的姓名" />
        </a-form-item>
        <a-form-item
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
          label="姓名"
        >
          <a-input v-decorator="['phoneNumber',]" placeholder="输入您的手机号" />
        </a-form-item>
        <a-form-item
          label="密码"
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
          class="stepFormText"
          hasFeedback
        >
          <a-input
            v-decorator="[
                  'password',
                  {rules: [{ required: true, message: '请输入密码(20位以内)',max:20 },{validator: handlePass,trigger: 'change'}]}
                ]"
            name="password"
            type="password"
          />
        </a-form-item>
        <a-form-item
          label="确认密码"
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
          class="stepFormText"
          hasFeedback
        >
          <a-input
            v-decorator="[
                  'confirm_password',
                  {rules: [{ required: true, message: '请输入确认密码' },{validator: handleConfirmPass,trigger: 'change'}]}
                ]"
            name="confirm_password"
            type="password"
          />
        </a-form-item>
        <a-form-item
          label="角色权限"
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
        >
          <a-select
            v-decorator="[
                  'permission',
                  {rules: [{ required: true, message: '请选择权限'},]}
                ]"
            placeholder
            style="width: 100%"
            @change="UserChange"
          >
            <a-select-option v-for="item in filteredOptions" :key="item" :value="item">{{ item }}</a-select-option>
          </a-select>
        </a-form-item>
      </a-form>
      <template slot="footer">
        <a-button
          class="sureButton"
          :style="{'margin-right':'20px'}"
          type="primary"
          @click="handleSubmit"
        >确认</a-button>
        <a-button class="cancelButton" @click="Submitcancel">取消</a-button>
      </template>
    </a-modal>
  </div>
</template>

<script>
const OPTIONS = ['Apples', 'Nails', 'Bananas', 'Helicopters']
const columns = [
  {
    title: '帐号',
    dataIndex: 'name',
    scopedSlots: { customRender: 'name' }
  },
  {
    title: '姓名',
    className: 'column-money',
    dataIndex: 'money'
  },
  {
    title: '手机号',
    dataIndex: 'address'
  },
  {
    title: '创建时间',
    dataIndex: 'creatime'
  },
  {
    title: '上次登录',
    dataIndex: 'lasttime'
  },
  {
    title: '角色权限',
    dataIndex: 'permission'
  },

  {
    title: '操作',
    scopedSlots: { customRender: 'opction' }
  }
]

const data = [
  {
    key: '1',
    name: 'John Brown',
    money: '￥300,000.00',
    address: 'New York No. 1 Lake Park'
  },
  {
    key: '2',
    name: 'Jim Green',
    money: '￥1,256,000.00',
    address: 'London No. 1 Lake Park'
  },
  {
    key: '3',
    name: 'Joe Black',
    money: '￥120,000.00',
    address: 'Sidney No. 1 Lake Park'
  }
]

export default {
  data() {
    return {
      data,
      columns,
      //  添加帐号弹窗
      Addaccount: false,
      formItemLayout: {
        labelCol: { span: 4 },
        wrapperCol: { span: 12 }
      },
      formTailLayout: {
        labelCol: { span: 4 },
        wrapperCol: { span: 8, offset: 4 }
      },
      password: '',
      form: this.$form.createForm(this),
      //  权限
      selectedItems: []
    }
  },
  methods: {
    //  角色权限选择改变
    UserChange(selectedItems) {
        console.log(selectedItems)
      this.selectedItems = selectedItems
    },
    //  搜索
    onSearch(value) {
      console.log(value)
    },
    // 添加帐号
    showModal() {
      this.Addaccount = true
    },
    // 提交表单
    handleSubmit(e) {
      e.preventDefault()
      this.form.validateFieldsAndScroll((err, values) => {
        // if (!err) {
        //   console.log('Received values of form: ', values)
        // }
        console.log(values)
      })
    },
    // 取消提交置空
    Submitcancel() {
      console.log('置空表单')
      this.form.resetFields()
    },
    handleOk(e) {
      console.log(e)
      this.Addaccount = false
    },
    // 输入密码校验
    handlePass(rule, value, callback) {
      this.password = value
      callback()
    },
    // 确认密码校验
    handleConfirmPass(rule, value, callback) {
      if (this.password && this.password !== value) {
        callback('两次密码输入不一致！')
      }
      // Note: 必须总是返回一个 callback，否则 validateFieldsAndScroll 无法响应
      callback()
    }
  },
  computed: {
    filteredOptions() {
      return OPTIONS.filter(o => !this.selectedItems.includes(o))
    }
  }
}
</script>
<style>
#Accountsettings .ant-table {
  border-left: 1px solid #dcdcdc;
  border-right: 1px solid #dcdcdc;
  border-radius: 4px;
}
#Accountsettings .ant-table-thead > tr > th {
  color: white;
  background: #1990ff !important;
}
#Accountsettings .ant-table th {
  text-align: center !important;
}
#Accountsettings .ant-table td {
  text-align: center !important;
}
.ant-modal-footer {
  border-top: none;
}
.ant-modal-body .ant-modal-confirm-btns {
  float: none;
  display: flex;
  justify-content: center;
}
.ant-modal-content {
  border-radius: 6px;
}
.ant-modal-header {
  border-radius: 6px;
}
.ant-modal-footer {
  text-align: center;
}
.sureButton {
  width: 100px;
  height: 32px;
  background: rgba(25, 144, 255, 1);
  opacity: 1;
}
.cancelButton {
  width: 100px;
  height: 32px;
  border: 1px solid rgba(204, 204, 204, 1);
  opacity: 1;
}
</style>