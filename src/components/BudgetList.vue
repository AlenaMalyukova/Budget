<template>
  <div class="budget-list-wrap">
    <ElCard :header="header">
      <BudgetListFilter @filter="filter"/>
      <template v-if="!isEmpty">
        <BudgetListItem 
          v-for="(item, prop) in list"
          :item="item"
          :key="prop"
          @deleteItem="deleteItem"/>
      </template>
      <el-alert v-else type="info" :title="emptyTitle" :closable="false"/>
    </ElCard>
  </div>
</template>

<script>
import BudgetListItem from './BudgetListItem'
import BudgetListFilter from './BudgetListFilter'
export default {
  name: "BudgetList",
  components: {
    BudgetListItem,
    BudgetListFilter
  },
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    header: "Budget List",
    emptyTitle: "Empty List"
  }),
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id)
    },
    filter(type) {
      this.$emit('filter', type)
    }
  },
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length
    }
  },
}
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}

</style>