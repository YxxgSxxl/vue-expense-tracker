<script setup lang="ts">
import { defineProps } from 'vue';

const emit = defineEmits(['transactionDeleted']);

// TypeScript type values
interface Transaction {
        id: number;
        name: string;
        amount: number;
    }

// Defining all props we need
const props = defineProps<{
    transactions: Transaction[];
}>()

// Delete transaction
const deleteTransaction = (id: number) => {
    emit('transactionDeleted', id);
}
</script>

<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in props.transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            <span>{{ transaction.name }}</span>
            <span>{{ transaction.amount }}</span>
            <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
        </li>
    </ul>
</template>