<template>
  <div class="income-list">
    <IncomeItem v-for="data in state.sortedIncome" :key="data.id" :income="data" />
  </div>
</template>

<script>
import IncomeItem from "./IncomeItem.vue";
export default {
  components: {
    IncomeItem,
  },
  props: {
    state: Object,
  },
};
</script>

<style scoped>
.income-list {
  margin-top: 30px;
  padding: 15px;
}
</style>