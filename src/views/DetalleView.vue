<template>
   <TituloPrincipal titulo="Detalle de serie"/>
   <RouterLink to="/">Regresar</RouterLink>
   <div v-if="cargando">Cargando...</div>
   <div v-if="serie">
        <h2>{{ serie.name }}</h2>
        <img :src="serie?.image.original" :alt="serie?.name">

        <h4>Estado</h4>
        <div>{{ serie.status }}</div>

        <h4>Genero</h4>
        <div>{{ serie.genres.join(", ") }}</div>

        <h4>Calificacion</h4>
        <div>{{ serie.rating.average }}</div>
   </div>
</template>

<script setup lang='ts'>
    import { ref, onMounted } from 'vue';
    import TituloPrincipal from '../components/TituloPrincipal.vue';
    import { useRoute } from 'vue-router';
    import type { Serie } from '../interfaces/Serie.ts';

    const serie = ref<Serie | null>(null);
    const cargando = ref<boolean>(false);
    
    const route = useRoute();

    async function consumirSerie(): Promise<void> {
        try{
            const id = route.params.id;
            const res = await fetch(`https://api.tvmaze.com/shows/${id}`);
            const data = await res.json();
            serie.value = data;

        } catch (e){
            console.log("Error: ", e)
        } finally {
            cargando.value = false;
        }
    }

    onMounted(() => {
        consumirSerie();
    })
</script>

<style scoped>
img {
    width: 90%;
}
</style>