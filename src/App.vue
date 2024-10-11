<script setup lang="ts">
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from 'vue';

const transactions: any = ref([
    { id: 1, name: 'Flower', amount: -19.99 },
    { id: 2, name: 'Salary', amount: 299.99 },
    { id: 3, name: 'Pudding', amount: -2.99 },
])

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
});
</script>

<template>
  <div class="container">
    <Header />

    <Balance :total="total"/>
    <IncomeExpenses />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<style scoped>

</style>
