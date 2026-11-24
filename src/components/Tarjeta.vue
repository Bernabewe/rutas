<template>
    <RouterLink :to="`/detalle/${serie.id}`" class="enlace">
        <div class="tarjeta">
            <img :src="serie.image.medium" alt="">
            <div>
                <h2>{{ serie.name }}</h2>
                <span>{{ serie.status }}</span>
            </div>
        </div>
    </RouterLink>
</template>

<script setup lang="ts">
    import type { Serie } from "../interfaces/Serie"
    defineProps<{
        serie: Serie
    }>();
</script>

<style>
.tarjeta {
    display: flex;
    gap: 10px;
    border: 1px solid gray;
    border-radius: 8px;
    padding: 10px;
}

.tarjeta img {
    width: 50px;
}

.enlace{
    text-decoration: none;
    color: black;
}
</style>