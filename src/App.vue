<template>
  <div id="app">
    <TotalBalance :total="totalBalance"/>
    <Form v-on:change-submit="onSubmit" />
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
    list: JSON.parse(localStorage.getItem('list')) || {
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
      if (confirm('Удалить ?')) {
        this.$delete(this.list, id);
        this.setStorage(this.list);
      }
    },
    onSubmit(data) {
      const correctData = {...data, value: data.type === 'OUTCOME' ? Number(`-${+data.value}`) : data.value, id: Math.random(1000)}
      this.$set(this.list, correctData.id, correctData);
      this.setStorage(this.list)
    },
    setStorage(list) {
      localStorage.setItem('list', JSON.stringify(list));
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
:root {
  --color-outcome: hsl(0, 60%, 50%);
  --color-income: hsla(123, 59%, 51%, 0.973);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  min-height: 60vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
}
</style>
