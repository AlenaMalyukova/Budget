<template>
  <div class="filter-btn-wrap">
    <el-button size="small" @click="filter('income')">Only Income</el-button>
    <el-button size="small" @click="filter('outcome')">Only Outcome</el-button>
    <el-button size="small" @click="filter('all')">Show All</el-button>
  </div>
</template>
<script>
export default {
  name: 'BudgetListFilter',
  methods: {
    filter(type) {
      this.$emit('filter', type)
    } 
  }
}
</script>
<style scoped>
.filter-btn-wrap {
  display: flex;
  justify-content: start;
}
</style>