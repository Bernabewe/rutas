<template>
    <h1>{{ titulo }}</h1>
</template>

<script setup lang="ts">
    defineProps<{
        titulo: string
    }>();
</script>

<style scoped>
    h1 {
        color: Orange;
    }
</style>