<script setup>
import { ref, watch } from 'vue';

const emit = defineEmits(['charName']);

function actualizarName(){
  emit('charName', `${character.value.name}`);
}

const charId = defineProps({
  charId: Number
})

// const currentId = ref(1); // Comenzamos con el ID 1
const character = ref({
  name: '',
  image: ''
});

async function fetchCharacter() {
  try {
    const response = await fetch(`https://rickandmortyapi.com/api/character/${charId.charId}`);
    if (!response.ok) {
      throw new Error('Error al obtener el personaje');
    }
    character.value = await response.json();
  } catch (error) {
    console.error(error);
    character.value = null; // En caso de error, no mostramos personaje
  }
}

watch(charId, async () => {
  await fetchCharacter(); // Actualizamos la información del personaje
});

fetchCharacter(); // Cargamos el primer personaje al montar el componente
</script>

<template>
  <div class="character-info">
    <h2>Información del Personaje</h2>
    <div v-if="character">
      <p><strong>ID:</strong> {{ character.id }}</p>
      <p><strong>Nombre:</strong> {{ character.name }}</p>
      <p><strong>Especie:</strong> {{ character.species }}</p>
      <p><strong>Estado:</strong> {{ character.status }}</p>
      <img :src="character.image" alt="Imagen del personaje" />
    </div>
    <button @click="actualizarName">Enviar Nombre</button>
    <slot></slot>
  </div>
</template>

<style scoped>
.character-info {
  text-align: center;
}

.character-info img {
  max-width: 200px;
  height: auto;
}
</style>