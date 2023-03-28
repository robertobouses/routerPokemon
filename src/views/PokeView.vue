<script setup>
import axios from "axios";
import { ref } from "vue";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const router = useRouter();
const pokeSprite = ref({});
const pokeSprite2 = ref({});

const back = () => {
    router.push("/pokemons");
};

const getData = async () => {
    console.log(route.params.name);
    try {
        const { data } = await axios.get(
            `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
        );
        pokeSprite.value = data.sprites.front_default;
        
    } catch (error) {
        console.log(error);
        pokeSprite.value = null;
    }
};

const getData2 = async () => {
    console.log(route.params.name);
    try {
        const { data } = await axios.get(
            `https://pokeapi.co/api/v2/pokemon/${route.params.name}`
        );
        pokeSprite2.value = data.sprites.front_shiny;
        
    } catch (error) {
        console.log(error);
        pokeSprite2.value = null;
    }
};

getData();
getData2();
</script>

<template>
    <main class="text-center">
        <div v-if="pokeSprite">
            <img :src="pokeSprite" alt="" />
            <h1>Poke: {{ $route.params.name }}</h1>
        </div>
        <div v-if="pokeSprite2">
            <img :src="pokeSprite2" alt="" />
           
        </div>
        <h1 v-else>Pokemon no encontrado...</h1>
        <button @click="back()">Volver al listado</button>
    </main>
</template>