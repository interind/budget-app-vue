<template>
  <ElCard class="form-card">
    <ElForm name="form-buget"  @submit.prevent="" method="POST" @keydown.enter.prevent="changeSubmit" :model="formData" ref="addItemForm" :rules="rules" label-position="top">
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
      <ElButton native-type="submit" type="primary" @click="changeSubmit" :disabled="!isActive">Add</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>

export default {
  name: 'Form',
  data() {
    return {
      formData: {
        type: 'INCOME',
        comment: '',
        value: 0,
      },
      rules: {
        comment: [{required: true, min: 2, message: 'Please select comment', trigger: 'change'}],
        value: [{required: true, message: 'Please select value', trigger: 'blur'},
        {required: true, type: 'number', message: 'Please select number', trigger: 'change'}
        ],
      },
    }
  },
  methods: {
    changeSubmit() {
      this.$refs['addItemForm'].validate((valid) => {
        if (valid) {
          this.$emit('change-submit', { ...this.formData });
          this.$refs['addItemForm'].resetFields();
        } else {
          return new Error('Что-то пошло не так');
        }
      })
    },
  },
  computed: {
    isActive() {
      return Boolean(this.formData.value > 0);
    }
  }
}
</script>

<style scoped>
  .form-card {
    flex-basis: 20%;
    order: 2;
    align-self: stretch;
  }
  .type-select {
    width: 100%;
  }
</style>