<script setup>
import { reactive, ref } from "vue";

const inicio = reactive({
  name: 'Inicio'
})
const series = ref('Series');
const varPesoFuente = ref('textoNegrita');
const urlLogo = reactive({
  url: 'public/logoNetflix.png'
});
let cssLiSubrayado = reactive({
  st: {
    style: {
    'text-decoration': 'overline',
    'font-style': 'italic'
    }
  }
})
</script>

<template>
  <header>
    <img style="width: 150px; height: 70%;" v-bind:src="urlLogo.url" alt="">
    <nav id="navHeader">
      <ul id="linksNav">
        <li :class="varPesoFuente">{{ inicio.name }}</li>
        <li v-bind="cssLiSubrayado.st">{{ series }}</li>
        <li>Peliculas</li>
        <li>Novedades populares</li>
        <li>Mi lista</li>
        <li>Explora por idiomas</li>
      </ul>
    </nav>
  </header>
</template>

<style scoped>
header {
  background-image: linear-gradient(to bottom, #5a5e62, #818387d2, #aaabadb9, #d4d4d59f, #ffffff81);
  height: 70px;
  width: 100vw;
  padding: 0 2%;
}
#navHeader{
  width: 60vw;
}
#linksNav{
  display: flex;
  justify-content: space-around;
  align-items: center;
  list-style: none;
}
.textoNegrita{
  font-weight: bold;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
