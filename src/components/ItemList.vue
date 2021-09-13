<template>
  <div v-if="!isEmpty">
    <ul class="list-item" v-for="(item, prop) in list" :key="prop">
      <li class="list-i"><span class="budget-comment">{{ item.comment }}</span></li>
      <li class="list-i"><span class="budget-value">{{ item.value }}</span></li>
      <li class="list-i"><ElButton type="danger" @click="deleteItem(item.id)" size="mini">Delete</ElButton></li>
    </ul>
  </div>
  <ElAlert v-else type="info" :title="emptyTitle" :closable="false"/>
</template>

<script>
export default {
  name: "ItemList",
  data: () => ({
    emptyTitle: "Список пустой",
  }),
  props: {
    list: {
      type: Object,
      default: () => ({})
    },
    isEmpty: {
      type: Boolean,
      default: () => false,
    },
    deleteItem: Function,
    default: () => {},
  },
}
</script>

<style scoped>
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
</style>