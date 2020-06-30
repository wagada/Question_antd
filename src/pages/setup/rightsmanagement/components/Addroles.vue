<template>
  <div>
    <!-- <a-button type="primary" @click="showModal">
      Open Modal with async logic
    </a-button>-->
    <a-button @click="showModal" class="roles">添加角色</a-button>
    <a-modal
      title="权限添加"
      :visible="visible"
      :confirm-loading="confirmLoading"
      @ok="handleOk"
      @cancel="handleCancel"
    >
      <a-form :form="form">
        <a-form-item
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
          label="角色"
        >
          <a-input
            v-decorator="[
          'username',
          { rules: [{ required: true, message: '请输入角色名称',trigger: 'blur' }] },
        ]"
            placeholder
          />
        </a-form-item>
        <a-form-item
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
          label="权限"
        >
          <a-checkbox-group
            v-decorator="['permission_group', { initialValue: ['A', 'B'] }]"
            style="width: 100%;"
          >
            <a-row>
              <a-col :span="12">
                <a-checkbox value="A">首页</a-checkbox>
              </a-col>
              <a-col :span="12">
                <a-checkbox disabled value="B">小程序管理</a-checkbox>
              </a-col>
              <a-col :span="12">
                <a-checkbox value="C">题库管理</a-checkbox>
              </a-col>
              <a-col :span="12">
                <a-checkbox value="D">答卷管理</a-checkbox>
              </a-col>
              <a-col :span="12">
                <a-checkbox value="E">用户管理</a-checkbox>
              </a-col>
              <a-col :span="12">
                <a-checkbox value="F">设置</a-checkbox>
              </a-col>
            </a-row>
          </a-checkbox-group>
        </a-form-item>
      </a-form>

      <template slot="footer">
        <a-button class="sureButton" @click="handleOk">确定</a-button>
        <a-button :style="{'width':'100px'}" class="cancelButton" @click="handleCancel">取消</a-button>
      </template>
    </a-modal>
  </div>
</template>
<script>
const formItemLayout = {
  labelCol: { span: 4 },
  wrapperCol: { span: 12 }
}
const formTailLayout = {
  labelCol: { span: 4 },
  wrapperCol: { span: 8, offset: 4 }
}
export default {
  data() {
    return {
      ModalText: 'Content of the modal',
      visible: false,
      confirmLoading: false,
      formItemLayout,
      formTailLayout,
      form: this.$form.createForm(this, { name: 'roles' })
    }
  },
  methods: {
    showModal() {
      this.visible = true
    },
    handleOk(e) {
      this.ModalText = 'The modal will be closed after two seconds'
      this.confirmLoading = true
      setTimeout(() => {
        this.visible = false
        this.confirmLoading = false
      }, 2000)
    },
    handleCancel(e) {
      console.log('Clicked cancel button')
      this.visible = false
    }
  }
}
</script>

<style>
.sureButton {
  width: 100px;
  height: 32px;
  background: rgba(25, 144, 255, 1);
  opacity: 1;
  color: white;
}
.sureButton:hover {
  background: rgb(12, 129, 238);
  color: white;
}
.cancelButton {
  width: 100px;
  height: 32px;
  border: 1px solid rgba(204, 204, 204, 1);
  opacity: 1;
}
.ant-modal-footer {
  border-top: none;
  text-align: center;
}
</style>
