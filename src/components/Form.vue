<template>
  <ElCard class="form-card">
    <ElForm :model="formData" ref="addItemForm" :rules="rules" label-position="top">
      <ElFormItem label="Тип бюджета" prop="type">
        <ElSelect class="type-select" v-model="formData.type" placeholder="Choose type...">
          <ElOption label="Доход" value="INCOME" />
          <ElOption label="Расход" value="OUTCOME" />
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Комментарий" prop="comment">
        <ElInput v-model="formData.comment"/>
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
        <ElInput v-model.number="formData.value" />
      </ElFormItem>
      <ElButton type="primary" :disabled="!isActive" @click="onSubmit">Submit</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>

export default {
  name: 'Form',
  data: () => ({
    formData: {
      type: 'INCOME',
      comment: '',
      value: 0,
    },
    rules: {
      comment: [{required: true, min: 2, message: 'Please select comment', trigger: 'change'}],
      value: [{required: true, message: 'Please select value', trigger: ['blur', 'change']},
      {required: true, type: 'number', message: 'Please select number', trigger: 'change'}
      ],
    }
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate((valid) => {
        console.log(this.$refs.addItemForm);
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      })
    },
  },
  computed: {
    isActive() {
      return Boolean(this.formData.value);
    }
  }
}
</script>

<style scoped>
  .form-card {
    flex-basis: 30%;
    align-self: flex-start;
  }
  .type-select {
    width: 100%;
  }
</style>