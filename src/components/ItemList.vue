<template>
  <div class="list" v-if="!isEmpty">
    <ul class="list-item" v-for="(item, prop) in list" :key="prop">
      <li class="list-i"><i class="el-icon-edit"/><span class="list-comment">{{ item.comment }}</span></li>
      <li class="list-i"><span :class="statusValue(item.value)">{{ item.value }}</span></li>
      <li class="list-i"><ElButton type="danger" icon="el-icon-delete" @click="deleteItem(item.id)" size="mini" plain>Delete</ElButton></li>
    </ul>
  </div>
  <ElAlert v-else type="info" :title="emptyTitle" :closable="false"/>
</template>

<script>
export default {
  name: "ItemList",
  data: () => ({
    emptyTitle: "Список пустой",
    statusValue: (value) => value < 0 ? "list-value list-value_min" : "list-value",
  }),
  props: {
    list: {
      type: Object,
      default: () => ({}),
      validator(value) {
        if (!localStorage.getItem('list')) {
          localStorage.setItem('list', JSON.stringify(value));
          return value;
        } else {
          return value;
        }
      }
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
  .list {
    max-height: 50vh;
    overflow-y: auto;
  }
  .list-item {
    display: flex;
    align-items: center;
    justify-content: space-around;
    list-style: none;
    padding: 10px 15px;
  }
  .list-value {
    font-weight: bold;
    color: var(--color-income);
  }

  .list-value_min {
    color: var(--color-outcome);
  }
  .list-i {
    flex-basis: 30%;
  }
  .list-i:first-child {
    text-align: start;
  }
  .list-i:last-of-type {
    flex-basis: 10%;
  }
</style>