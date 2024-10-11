<script setup lang="ts">
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed, onMounted } from 'vue';
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

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions') || '[]') as Transaction[];

  if(savedTransactions) {
    transactions.value = savedTransactions;
  }
});

/*
  component: Balance.vue
  work: Get total
*/
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0)
});

const calculateIncomeExpenses = (condition: (transaction: Transaction) => boolean): string => {
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

  saveTransactionsToLocalStorage();

  toast.success('Transaction Added')
}

// Delete transaction
const handleTransactionDeleted = (id: number) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  saveTransactionsToLocalStorage();

  toast.success('Transaction Deleted');
}

// Save to localStorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
}
</script>

<template>
  <div class="container">
    <Header />

    <Balance :total="total"/>
    <IncomeExpenses :income="+income" :expenses="+expenses"/>
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
</template>
