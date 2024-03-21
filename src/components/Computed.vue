<script setup>
import { reactive, computed, onMounted, ref, onBeforeUnmount } from "vue";

let alumno = reactive({
  name: "Eduardo",
  materias: ["Logica", "HTML", "Javascript"],
});

let alumnoTieneMaterias = computed(() => {
  return alumno.materias.length > 0 ? "Si" : "No";
});

let contador  = ref(0);

let intervalo;

// onMounted(() => {
//     intervalo = setInterval(() => {
//     contador.value++;
//     console.log(contador.value);
//   }, 1000);
// })

// onBeforeUnmount(() => {
//   clearInterval(intervalo);
// })

let inputField = ref(null);

const hacerFocus = () => {
    console.log(inputField.value);
    if (inputField.value) {
        inputField.value.focus();
        inputField.value.value = "Hola Mundo"
    }
}
</script>

<template>
    <section>
     {{ alumno.name }} - {{ alumnoTieneMaterias }} tiene materias.
     <button @click="alumno.materias.pop(); console.log(alumno.materias);">Eliminar Materia</button>
    </section>
    <hr>
    <input type="text" :ref="(el) => {inputField = el}" placeholder="Escribe algo..." >
    <button @click="hacerFocus">Hacer Focus</button>
</template>