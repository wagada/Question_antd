<template>
  <div>
    <a @click="showModal" :style="{'color':'#63C83B'}" type="link">添加节</a>
    <a-modal
      title="增加节"
      v-model="AddsubjectVisible"
      :confirm-loading="confirmLoading"
      okText="保存"
      cancelText="取消"
      @ok="handleSubmit"
      @cancel="handleCancel"
    >
      <!-- 添加行业表单 -->
      <a-form
        :form="form"
        :label-col="{ span: 4 }"
        :wrapper-col="{ span: 11 }"
        @submit="handleSubmit"
      >
        <a-form-item label>
          <!-- <a-input v-decorator="['name', { rules: [{ required: true, message: '请输选择所属!' }] }]" /> -->
          <a-select
            v-decorator="[
          'name',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
            placeholder="行业"
          >
            <a-select-option value="male">male</a-select-option>
            <a-select-option value="female">female</a-select-option>
          </a-select>
        </a-form-item>

        <a-form-item label>
          <!-- <a-input v-decorator="['name', { rules: [{ required: true, message: '请输选择所属!' }] }]" /> -->
          <a-select
            v-decorator="[
          'subject',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
            placeholder="科目"
          >
            <a-select-option value="male">male</a-select-option>
            <a-select-option value="female">female</a-select-option>
          </a-select>
        </a-form-item>

        <a-form-item label>
          <!-- <a-input v-decorator="['name', { rules: [{ required: true, message: '请输选择所属!' }] }]" /> -->
          <a-select
            v-decorator="[
          'subject',
          { rules: [{ required: true, message: 'Please select your gender!' }] },
        ]"
            placeholder="章"
          >
            <a-select-option value="male">male</a-select-option>
            <a-select-option value="female">female</a-select-option>
          </a-select>
        </a-form-item>

        <a-form-item label="名称">
          <a-input v-decorator="['name', { rules: [{ required: true, message: '请输入名称!' }] }]" />
        </a-form-item>
        <a-form-item label="排序 节">
          <a-input v-decorator="['name2', { rules: [{ required: true, message: '请输入章!' }] }]" />
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
      AddsubjectVisible: false,
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
          //   this.AddsubjectVisible = false
          this.confirmLoading = false
        }
      })
    },
    showModal() {
      this.AddsubjectVisible = true
    },
    handleOk(e) {
      this.ModalText = 'The modal will be closed after two seconds'
      this.confirmLoading = true
    },
    handleCancel(e) {
      console.log('Clicked cancel button')
      this.AddsubjectVisible = false
      this.$emit('visible', false)
    },
    handleSelectChange(value) {
      console.log(value)
      this.form.setFieldsValue({
        note: `Hi, ${value === 'male' ? 'man' : 'lady'}!`
      })
    }
  },
  created() {
    // this.AddIndustryVisible = this._props.visible
  },
  updated() {
    console.log(this._props.visible)
  }
}
</script>
