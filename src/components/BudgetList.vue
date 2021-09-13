<template>
  <div class="budget-list-wrap">
    <ElCard class="budget-card" :header="header">
      <ItemList :list="list" :isEmpty="isEmpty" :deleteItem="deleteItem"/>
    </ElCard>
  </div>
</template>

<script>
import ItemList from './ItemList'

export default ({
  name: "BudgetList",
  components: {
    ItemList,
  },
  data: () => ({
    header: "Budget List", // динамическое добавление header в элемент Card
  }),
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    }
  },
   methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    }
  }
})
</script>

<style scoped>
  .budget-list-wrap {
    flex-basis: 58%;
    align-self: stretch;
  }

  .budget-value {
    font-weight: bold;
  }
  .budget-card {
    height: 100%;
  }
</style>
