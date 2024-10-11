<script setup lang="ts">
let transactions: any[] = [
    { id: 1, name: 'Flower', amount: -19.99 },
    { id: 2, name: 'Salary', amount: 299.99 },
]
</script>

<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            <span>{{ transaction.name }}</span>
            <span>{{ transaction.amount }}</span>
            <button class="delete-btn">x</button>
        </li>

        <!-- <li class="minus">
            Cash <span>-$400</span>
            <button class="delete-btn">x</button>
        </li>
        <li class="plus">
            Paycheck <span>+$800</span>
            <button class="delete-btn">x</button>
        </li> -->
    </ul>
</template>

<style scoped>
</style>
