# Vue Expense Tracker  
This project is made with a youtube tutorial and adapted in Composition API and with TypeScript syntax  

## Status -> Project Done ✔️

## Documentations  

"TransactionList.vue" --> Passed the transactions list in a prop, with TypeScript syntax:  

```
<script setup lang="ts">
import { defineProps } from 'vue';

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
</script>

<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in props.transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            <span>{{ transaction.name }}</span>
            <span>{{ transaction.amount }}</span>
            <button class="delete-btn">x</button>
        </li>
    </ul>
</template>

<style scoped>
</style>
```  

And with vanilla Javascript:  

```
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    },
});
</script>

<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in props.transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            <span>{{ transaction.name }}</span>
            <span>{{ transaction.amount }}</span>
            <button class="delete-btn">x</button>
        </li>
    </ul>
</template>

<style scoped>
</style>
```