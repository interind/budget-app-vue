<template>
  <div class="budget-list-wrap">
    <ElCard class="budget-card" :header="header">
      <ElCheckboxGroup v-model="checkList" @change="changeCheckList">
        <ElCheckbox label="All" class=""/>
        <ElCheckbox label="INCOME" class=""/>
        <ElCheckbox label="OUTCOME" class=""/>
      </ElCheckboxGroup>
      <ItemList :list="arrFilter(list, checkList)" :isEmpty="isEmpty" :deleteItem="deleteItem"/>
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
  data: () => {
    const filterList = (list, checkList) => {
      const arr = {...list};
      const filterObject = {};
      if (checkList[0] !== 'All') {
        for (let i in arr) {
          if (arr[i].type === checkList[0]) {
            filterObject[i] = arr[i];
          }
        }
        return filterObject;
      }
      return arr;
    };
    return ({
      header: "Budget List", // динамическое добавление header в элемент Card
      checkList: ['All'],
      arrFilter: filterList
    })
  },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    }
  },
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
   methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },
    changeCheckList(arr) {
      this.checkList = [arr[arr.length - 1]];
    }
  }
})
</script>

<style scoped>

  .budget-list-wrap {
    flex-basis: 70%;
    order: 3;
    flex-grow: 2;
    align-self: stretch;
  }
  .budget-card {
    height: 100%;
  }

</style>
