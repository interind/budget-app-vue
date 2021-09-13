<template>
  <div id="app">
    <Form />
    <TotalBalance :total="totalBalance"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>

import Form from './components/Form';
import BudgetList from './components/BudgetList';
import TotalBalance from './components/TotalBalance';

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    list: {
      1: {
        type: 'INCOME',
        value: 100,
        comment: '#Комментарий доходов',
        id: 1
      },
      2: {
        type: 'OUTCOME',
        value: -50,
        comment: '#Комментарий расходов',
        id: 2
      },
    }
  }),
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    }
  },
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => acc + item.value, 0);
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
  background-color: #808080;
  min-height: 60vh;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}
</style>
