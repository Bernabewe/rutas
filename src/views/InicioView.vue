<template>
    <TituloPrincipal titulo="Series"/> 

    <button @click="consumirSeries()">Cargar Series</button>
    <div v-if="cargando">Cargando...</div>
    <div v-else>
        <Tarjeta 
            v-for="s in series"
            :key="s.id"
            :serie="s">
        </Tarjeta>
    </div>

</template>

<script setup lang="ts">
    import { onMounted, ref } from 'vue';
    import Tarjeta from '../components/Tarjeta.vue';
    import TituloPrincipal from '../components/TituloPrincipal.vue';
    import type { Serie } from '../interfaces/Serie.ts';

    const series = ref<Serie[]>([]);
    const cargando = ref<boolean>(false);

    // GET: https://api.tvmaze.com/shows

    async function consumirSeries() : Promise<void>{
        try {
            const res = await fetch("https://api.tvmaze.com/shows");
            const data = await res.json();
            console.log("data", data);
            series.value = data;
        } catch (e) {
            console.log(e);
        } finally {
            cargando.value = false;
        }
    }

    onMounted(() => {
        consumirSeries();
    })
</script>

<style scoped>

</style>