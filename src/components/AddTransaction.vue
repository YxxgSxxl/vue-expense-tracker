<script setup lang="ts">
    import { ref } from 'vue';
    import { useToast } from 'vue-toastification';

    const name = ref<string>('');
    const amount = ref<string>('');

    const emit = defineEmits(['transactionSubmitted']);
    const toast = useToast();

    const onSubmit = () => {
        if(!name.value || !amount.value) {
            toast.error('Both fields must be filled');
            return;
        } else if(isNaN(Number(amount.value))) {
            toast.error('Amount field must be a number (2, 2.5, -2)');
            return;
        } else {
            const transactionData = {
            name: name.value,
            amount: parseFloat(amount.value),
            }

            emit('transactionSubmitted', transactionData)
        }
    }
</script>

<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Name</label>
            <input type="text" id="text" v-model="name" placeholder="Enter Name...">
        </div>
        <div class="form-control">
            <label for="amount">
                Amount <br />
                <small>(negative = expense, positive = income)</small>
            </label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter amount...">
        </div>
        <button class="btn">Add Transaction</button>
    </form>
</template>