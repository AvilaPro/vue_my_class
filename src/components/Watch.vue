<script setup>
    import { ref, watch, watchEffect } from "vue";

    // let albumId = ref(0);

    let inputMensajeWatch = ref(null);

    let mensajeWatch = ref('');

    //Definicion de emit para enviar al padre
    const emit = defineEmits(['mensajeParaPapa']);

    //Definicion de props en el Hijo
    const props = defineProps({
        albumId: {
            type: String,
            default: '1'
        }
    })

    // watch(albumId, () => {
    //     fetch(`https://jsonplaceholder.typicode.com/albums/${albumId.value}`)
    //   .then(response => response.json())
    //   .then(json => {
    //     album.value = json;
    //   });
    //   inputId.value.value = '';
    //   inputId.value.focus();
    // }, {inmediate: true});

    watchEffect(async () => {
        await fetch(`https://jsonplaceholder.typicode.com/albums/${props.albumId}`)
      .then(response => response.json())
      .then(json => {
        album.value = json;
      });
    })

    let album = ref({
        userId : 0,
        id: 0,
        title: ''
    })

    const cambiarMensaje = () => {
        if (inputMensajeWatch.value) {
            mensajeWatch.value = inputMensajeWatch.value.value;
            console.log(mensajeWatch.value);
            emit('mensajeParaPapa', mensajeWatch.value);
        }
    }
</script>

<template>
    <hr>
    <br>
    <i>Watch Component</i><br>
    <input type="text" :ref="(el) => {inputMensajeWatch = el}">
    <button @click="cambiarMensaje">Cambiar Mensaje a Padre</button>
    <div style="display: flex; justify-content: center; padding: 25px 0; font-size: 3em;">
        Album ID: {{ album.id }}<br>
        Titulo: {{ album.title }}
    </div>
    <slot>En caso de no recibir del padre</slot><br>
    <i>Fin del Watch Component</i>
    <hr>
    <br>
</template>

<style scoped>
</style>