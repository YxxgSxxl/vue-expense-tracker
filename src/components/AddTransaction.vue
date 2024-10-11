<script setup lang="ts">
</script>

<template>
    <h3>Add new transaction</h3>
    <form id="form">
        <div class="form-control">
            <label for="text">Name</label>
            <input type="text" id="text" placeholder="Enter Name...">
        </div>
        <div class="form-control">
            <label for="amount">
                Amount <br />
                <small>(negative = expense, positive = income)</small>
            </label>
            <input type="number" id="amount" placeholder="Enter amount...">
        </div>
        <button class="btn">Add Transaction</button>
    </form>
</template>

<style scoped>
</style>
