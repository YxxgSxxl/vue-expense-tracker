<script setup lang="ts">
import { defineProps } from 'vue';

const props = defineProps({
    total: {
        type: Number,
        required: true,
    }
})
</script>

<template>
    <h4>Your balance</h4>
    <h1 id="balance">${{ props.total }}</h1>
</template>

<style scoped>
</style>
