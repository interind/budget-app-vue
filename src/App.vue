<template>
  <div id="app">
    <TotalBalance :total="totalBalance"/>
    <Form @submitForm="onSubmit"/>
    <BudgetList :list="list" @deleteItem="onDeleteItem"/>
  </div>
</template>

<script>

import BudgetList from './components/BudgetList';
import Form from './components/Form';
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
    },
    onSubmit(data) {
      const info = {...data, id: Math.random(1000)};
      this.$set(this.list, info.id, info);
    }
  },
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => acc + item.value, 0);
    }
  }
}
</script>

<style scoped>
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
  justify-content: space-around;
}
</style>
