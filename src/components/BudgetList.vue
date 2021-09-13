<template>
  <div class="budget-list-wrap">
    <ElCard class="budget-card" :header="header">
      <template v-if="!isEmpty">
        <ul class="list-item" v-for="(item, prop) in list" :key="prop">
          <li class="list-i"><span class="budget-comment">{{ item.comment }}</span></li>
          <li class="list-i"><span class="budget-value">{{ item.value }}</span></li>
          <li class="list-i"><ElButton type="danger" @click="deleteItem(item.id)" size="mini">Delete</ElButton></li>
        </ul>
      </template>
      <ElAlert v-else type="info" :title="emptyTitle" :closable="false"/>
    </ElCard>
  </div>
</template>

<script>

export default ({
  name: "BudgetList",
  data: () => ({
    header: "Budget List", // динамическое добавление header в элемент Card
    emptyTitle: "Список пустой",
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
  .list-item {
    display: flex;
    align-items: center;
    justify-content: space-around;
    list-style: none;
    padding: 10px 15px;
  }
  .list-i {
    flex-basis: 30%;
  }
  .list-i:last-of-type {
    flex-basis: 10%;
  }
  .budget-value {
    font-weight: bold;
  }
  .budget-card {
    height: 100%;
  }
</style>
