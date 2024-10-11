<script setup lang="ts">
import { defineProps } from 'vue';

// Defining all props we need
const props = defineProps({
    income: {
        type: Number,
        required: true,
    },

    expenses: {
        type: Number,
        required: true,
    }
});
</script>

<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="money-plus" class="money plus">+${{ props.income }}</p>
        </div>
        <div>
            <h4>Expenses</h4>
            <p id="money-minus" class="money minus">-${{ props.expenses * -1 }}</p>
        </div>
    </div>
</template>