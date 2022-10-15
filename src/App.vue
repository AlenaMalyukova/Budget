<template>
  <div id="app">
    <Form @submitForm="onFormSubmit"/>
    <TotalBalance :total="totalBalance"/>
    <BudgetList 
      :list="filteredList" 
      @deleteItem="onDeleteItem"
      @filter="filter"
      />
  </div>
</template>

<script>
import BudgetList from './components/BudgetList'
import TotalBalance from './components/TotalBalance'
import Form from './components/Form'

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form,
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: 'Some comment',
        id: 1,
      },
      2: {
        type: 'OUTCOME',
        value: 50,
        comment: 'Some outcome comment',
        id: 2,
      }
    },
    filterType: 'all'
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => {
          if (item.type === 'INCOME') {
            return acc + item.value
          } else {
            return acc - item.value
          }
        }, 0
      )
    },
    filteredList() {
      if (this.filterType === 'outcome') {
        return this.filterList('OUTCOME')
      }

      if (this.filterType === 'income') {
        return this.filterList('INCOME')
      }

      return this.list
    }
  },
  methods: {
    filterList(type) {
      const arrList = Object.values(this.list)
      const filteredArrList = arrList.filter(i => i.type === type)
      const filteredObjList = Object.assign({}, filteredArrList)

      return filteredObjList
    },
    onDeleteItem(id) {
      this.$delete(this.list, id)
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };

      this.$set(this.list, newObj.id, newObj)
    },
    filter(type) {
      this.filterType = type
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
