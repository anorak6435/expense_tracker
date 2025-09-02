<template>
  <li class="transaction" :class="{ expense: amount < 0, income: amount >= 0 }">
    <span>{{ description }}</span>
    <span>{{ when }}</span>
    <span>{{ from }}</span>
    <span>{{ to }}</span>
    <span
      ><span v-if="is_income">+</span> <span v-else>-</span> €{{
        absolute
      }}</span
    >
  </li>
</template>

<script>
export default {
  name: "TransactionComp",
  props: {
    description: String,
    when: String,
    from: String,
    to: String,
    amount: Number,
  },
  computed: {
    is_income() {
      return this.amount >= 0;
    },
    absolute() {
      return Math.abs(this.amount);
    },
  },
};
</script>

<style>
</style>