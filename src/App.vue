<script setup lang="ts">
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast();

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

/*
  component: Balance.vue
  work: Get total
*/
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

/*
  component: IncomeExpenses.vue
  work: Get income and expenses
*/
const income = computed(() => calculateIncomeExpenses(transaction => transaction.amount > 0));

const expenses = computed(() => calculateIncomeExpenses(transaction => transaction.amount < 0));

/*
  component: AddTransaction.vue
  work: Generate unique ID
*/
const generateUniqueId = (): number => {
  return Math.floor(Math.random() * 1000000);
}

/*
  component: AddTransaction.vue
  work: Add transactions
*/
interface TransactionData {
  name: string;
  amount: number;
}

/*
  component: AddTransaction.vue
  work: Handle values of submitted form
*/
const handleTransactionSubmitted = (transactionData: TransactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    name: transactionData.name,
    amount: transactionData.amount,
  });

  toast.success('Transaction Added')
}
</script>

<template>
  <div class="container">
    <Header />

    <Balance :total="total"/>
    <IncomeExpenses :income="+income" :expenses="+expenses"/>
    <TransactionList :transactions="transactions" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>
