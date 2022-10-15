<template>
  <div>
    <div class="list-item">
      <span class="budget-comment">{{item.comment}}</span>
      <span class="budget-value">
        <i :class="isIncome"></i>
        {{item.value}}
      </span>
      <ElButton type="danger" size="mini" @click="dialogVisible = true">Delete</ElButton>
      <el-dialog title="Notification" :visible.sync="dialogVisible" width="30%" :before-close="closeDialog">
        <span>Are you sure to delete this item?</span>
        <span slot="footer" class="dialog-footer">
          <el-button @click="closeDialog">Cancel</el-button>
          <el-button type="primary" @click="deleteItem(item.id)">Confirm</el-button>
        </span>
      </el-dialog>
    </div>
  </div>
</template>
<script>
export default {
  name: 'BudgetListItem',
  props: {
    item: Object
  },
  data: () => ({
    dialogVisible: false
  }),
  methods: {
    deleteItem(id) {
        this.$emit('deleteItem', id)
    },
    closeDialog() {
      this.dialogVisible = false
    },
  }, 
  computed: {
    isIncome() {
      if(this.item.type === 'INCOME') {
        return 'el-icon-caret-top'
      } else {
        return 'el-icon-caret-bottom'
      }
    }
  }
}
</script>
<style scoped>
.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
.el-icon-caret-top {
  color:green
}
.el-icon-caret-bottom {
  color: red
}
</style>