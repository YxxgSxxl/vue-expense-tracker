<script setup lang="ts">
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref } from 'vue';

let transactions: any = ref([
    { id: 1, name: 'Flower', amount: -19.99 },
    { id: 2, name: 'Salary', amount: 299.99 },
    { id: 3, name: 'Pudding', amount: -2.99 },
])
</script>

<template>
  <div class="container">
    <Header />

    <Balance />
    <IncomeExpenses />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<style scoped>

</style>
