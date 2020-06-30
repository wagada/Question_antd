<template>
  <div>
    <!-- <a-button type="primary" @click="showModal">添加行业</a-button>
     -->
     <a @click="showModal" :style="{'margin-right':'10px'}" type="link">编辑</a>
    <a-modal
      title="编辑行业"
      v-model="EditIndustryVisible"
      :confirm-loading="confirmLoading"
      okText="保存"
      cancelText="取消"
      @ok="handleSubmit"
      @cancel="handleCancel"
    >
      <!-- 编辑行业表单 -->
      <a-form
        :form="form"
        :label-col="{ span: 5 }"
        :wrapper-col="{ span: 11 }"
        @submit="handleSubmit"
      >
        <a-form-item label="行业名称">
          <a-input v-decorator="['name', { rules: [{ required: true, message: '请输入行业名称!' }] }]" />
        </a-form-item>
        <a-form-item label="排序 行业">
          <a-input v-decorator="['name2', { rules: [{ required: true, message: '请输入行业!' }] }]" />
        </a-form-item>
      </a-form>
    </a-modal>
  </div>
</template>
<script>
export default {
  props: {
    visible: Boolean
  },
  data() {
    return {
      ModalText: 'Content of the modal',
      EditIndustryVisible: false,
      confirmLoading: false,
      form: this.$form.createForm(this, { name: 'coordinated' })
    }
  },
  methods: {
    handleSubmit(e) {
      e.preventDefault()
      this.confirmLoading = true
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values)
          return err
        } else {
          this.$emit('visible', false)
          //   this.EditIndustryVisible = false
          this.confirmLoading = false
        }
      })
    },
    showModal() {
      this.EditIndustryVisible = true
    },
    handleOk(e) {
      this.ModalText = 'The modal will be closed after two seconds'
      this.confirmLoading = true
    },
    handleCancel(e) {
      console.log('Clicked cancel button')
      this.EditIndustryVisible = false
      this.$emit('visible', false)
    }
  },
  created() {
    // this.AddIndustryVisible = this._props.visible
  },
  mounted() {
      console.log(this._props)
  }
}
</script>
