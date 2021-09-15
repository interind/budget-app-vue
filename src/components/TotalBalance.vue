<template>
  <div class="total-value">Balance: <span :class="statusTotal(total)">{{ total }}</span></div>
</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    }
  },
  data: () => ({
    statusTotal: (total) => (total <= 0) ? 'total-value__num total-value__num_min' : 'total-value__num',
  }),
}
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: left;
  flex-basis: 100%;
  order: 1;
}
.total-value__num {
  color: var(--color-income);
}

.total-value__num_min {
  color: var(--color-outcome);
}

</style>