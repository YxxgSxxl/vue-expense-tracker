<script setup lang="ts">
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from 'vue';

// TypeScript type values
interface Transaction {
    id: number;
    name: string;
    amount: number;
}

// Get transactions
const transactions = ref<Transaction[]>([])

// const transactions: any = ref([
//     { id: 1, name: 'Flower', amount: -19.99 },
//     { id: 2, name: 'Salary', amount: 299.99 },
//     { id: 3, name: 'Pudding', amount: -2.99 },
// ])

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
});

const calculateIncomeExpenses = (condition) => {
  return transactions.value
    .filter(condition)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
};

// Get incomes
const income = computed(() => calculateIncomeExpenses(transaction => transaction.amount > 0));

// Get expenses
const expenses = computed(() => calculateIncomeExpenses(transaction => transaction.amount < 0));
</script>

<template>
  <div class="container">
    <Header />

    <Balance :total="total"/>
    <IncomeExpenses :income="income" :expenses="expenses"/>
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<style scoped>

</style>
