<template>
  <el-card class="form-card">
    <el-form :model="formData" ref="addItemForm" :rules="rules">
      <el-form-item label="Type" prop="type">
        <el-select class="type-select" v-model="formData.type" placeholder="Choose type...">
          <el-option label="Income" value="INCOME"/>
          <el-option label="Outcome" value="OUTCOME" />
        </el-select>
        <el-form-item label="Comments" prop="comment">
          <el-input v-model="formData.comment" />
        </el-form-item>
        <el-form-item label="Value" prop="value">
          <el-input v-model.number="formData.value" />
        </el-form-item>
        <el-button class="submit-btn" type="primary" size="medium" @click="onSubmit">Submit</el-button>
      </el-form-item>
    </el-form>
  </el-card>
</template>

<script>
export default {
  name: "Form",
  data: () => ({
    formData: {
      type: '',
      comment: '',
      value: 0
    },
    rules: {
      type: [
        { required: true, message: 'Please select type', trigger: "blur"}
      ],
      comment: [
        { required: true, message: 'Please input comment', trigger: "change" }
      ],
      value: [
        { required: true, message: 'Please input value', trigger: "change" },
        { min: 1, type: 'number', message: 'Value must be a greater than zero', trigger: 'change'}
      ]
    }
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if(valid) {
          this.$emit('submitForm', {...this.formData}),
          this.$refs.addItemForm.resetFields()
        }
      })
    },
  }
}
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
}

.type-select {
  width: 100%;
}

.submit-btn {
  margin-top: 20px;
}
</style>