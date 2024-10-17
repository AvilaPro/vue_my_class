<script setup>
import { ref } from "vue";
import RickAndMorty from "./RickAndMorty.vue";

const currentId = ref(1);
const nameChar = ref('');

function incrementId() {
  currentId.value += 1; // Incrementamos el ID
}
</script>

<template>
    <h1 v-if="nameChar != ''">El nombre del personaje es: {{ nameChar }}</h1>

    <RickAndMorty :charId="currentId" @charName="(name) => nameChar = name">
        <h3>
            <strong>created By <i>AvilaPro</i></strong>
        </h3>
    </RickAndMorty>
    <button @click="incrementId">Siguiente Personaje</button>
</template>

<style scoped>

</style>