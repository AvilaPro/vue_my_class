<script setup>
import { computed, onMounted, onUnmounted, onUpdated, reactive, ref } from "vue";

    //variable reactiva para el control de tiempo
    const tiempo = ref(0);
    //variable que contendra el intervalo del temporizador.
    let intervalo = null;
    //variable ref de items frutas
    const itemsFrutas = ref([]);
    //variable que toma el indice de la fruta seleccionada en el input
    const indiceFruta = ref(0);
    //input de entrada de seleccion
    const inputFruta = ref("");

    //variables reactiva de objeto
    const usuario = reactive({
        name: 'Eduardo',
        lastname: 'Mejias'
    });
    const frutas = reactive([
        { id: 1, name: 'Manzana' },
        { id: 2, name: 'Platano' },
        { id: 3, name: 'Naranja' }
    ])
    // variables ref
    const userName  = ref('Luis');
    const userLastname = ref('Avila');
    // variable computada reactiva
    const nombreReactivo = computed({
        get() {
            return usuario.name + ' ' + usuario.lastname;
        },
        set(value) {
            [usuario.name, usuario.lastname] = value.split(' ');
        }
    });
    const fruits = computed({
        get() {
            return frutas.map((fruit) => fruit.name);
        },
        set(value) {
            for(let i = 0; i < frutas.length; i++){
                frutas[i].name = value[i];
            }
        }
    })
    // variable computada ref

    //funcion que cambia la computada
    function changeName() {
        fruits.value = ['Limon', 'Fresa', 'Mango'];

    }
    //funcion que cambia el indice seleccionado de la fruta
    function changeIndiceFruta() {
        console.log(itemsFrutas);
        indiceFruta.value = parseInt(inputFruta.value) - 1;
        for(let i = 0;  i < frutas.length; i++){
            if(indiceFruta.value ==  i){
                //le cambio el color al li que coincide
                itemsFrutas.value[i].style.color = 'red';
            }else{
                itemsFrutas.value[i].style.color = 'black';
            }
        }
    }

    //manejadores de eventos para cuando se monta y se desmonta el componente
    onMounted(() => {
        intervalo = setInterval(() => {
            tiempo.value++;
        }, 1000);
    })

    onUpdated(() => {
        // tiempo.value = 100;
    })

    onUnmounted(() => {
        clearInterval(intervalo);
    })
</script>

<template>
    <h1>El tiempo transcurrido es: {{ tiempo }} segundo</h1>
    <h3 style="text-align: center;">Nombre computado {{ nombreReactivo }}</h3>
    <h3 style="text-align: center; color: blue; font-weight: bold;">Frutas no computado {{ frutas }}</h3>
    <h3 style="text-align: center; color: red; font-weight: bold;">Frutas computado {{ fruits }}</h3>
    <div style="display: flex; justify-content: center;">
        <button @click="changeName">Cambiar computada</button>
    </div>
    <div style="display: flex; justify-content: center;">
        <ul>
            <li v-for="frut in frutas" :key="frut.id" ref="itemsFrutas">
                {{ frut.id }} - {{ frut.name }}
            </li>
        </ul>
    </div>
    <div style="display: flex; justify-content: center;">
        <select name="" id="" v-model="inputFruta">
            <option v-for="frut in frutas" :key="frut.id" :value="frut.id">{{ frut.name }}</option>
        </select>
        <button @click="changeIndiceFruta">Tomar Fruta</button>
    </div>
</template>

<style scoped>

</style>