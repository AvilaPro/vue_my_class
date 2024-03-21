<script setup>
import { reactive, ref, onMounted, onUpdated, onBeforeUnmount } from "vue";

//Componentes importados
import Computed from "./components/Computed.vue";
import Watch from "./components/Watch.vue";

//Atributos del componente (ref, reactive)
const inicio = reactive({
  btn1: "Inicio",
  btn2: "Series",
  btn3: "Peliculas",
  btn4: "Novedades Populares",
  btn5: "Mi Lista",
  btn6: "Explora por idiomas",
});
const series = ref("Series");
const varPesoFuente = ref("textoNegrita");
const urlLogo = reactive({
  url: "public/logoNetflix.png",
});
let cssLiSubrayado = reactive({
  st: {
    style: {
      "text-decoration": "overline",
      "font-style": "italic",
    },
  },
});

let banner = reactive({
  title: "ONE PIECE",
  subTitle: "Adventure will continue",
});
let colorTxtBanner = ref("colorTxtBanner");

//atributos del formulario de login
//input text: nombre
let nombreRegistro = ref("");
//input radio: sexo
let male = ref("Masculino");
let female = ref("Femenino");
let sexoSeleccionado = ref("Masculino");
//input checkbox: preferencias
let prefers = ref([]);

//atributos clase 3 - v-for
let usuarios = ref([]);

let dejar = ref(true);

let inputId = ref(null);

let albumId = ref('1');

let mensajeDesdeWatch = ref('No se ha recibido mensaje desde Watch Component');

let algoParaSlot = ref('Esto es un dato para el slot');

/**
 * Scripts de ejecucion
 */
onMounted(() => {
  fetch("https://jsonplaceholder.typicode.com/users")
    .then((response) => response.json())
    .then((json) => {
      usuarios.value = json;
      console.log(usuarios.value);
    });
});

const cambiarID = () => {
  if (inputId.value) {
    albumId.value = inputId.value.value;
    console.log(albumId.value);
    //Limpieza del input en el padre
    inputId.value.value = '';
    inputId.value.focus();
  }
};
/**
 * //Metodos del componente
 */
function mostrarInfo(info) {
  alert(`Diste click en el boton ${info}`);
}
function mostrarEvent(event) {
  console.log(event);
  alert("Diste click en: " + event.target.innerHTML);
  s;
}
</script>

<template>
  <header @click.self="mostrarInfo('Click en el Header')">
    <img style="width: 150px; height: 70%" v-bind:src="urlLogo.url" alt="" />
    <nav id="navHeader">
      <ul id="linksNav">
        <li :class="varPesoFuente" v-on:click.stop="mostrarEvent">
          {{ inicio.btn1 }}
        </li>
        <li
          v-bind="cssLiSubrayado.st"
          v-on:click.stop="mostrarInfo(inicio.btn2)"
        >
          {{ inicio.btn2 }}
        </li>
        <li v-on:click.stop="mostrarInfo(inicio.btn3)">{{ inicio.btn3 }}</li>
        <li @click.stop="mostrarInfo(inicio.btn4)">{{ inicio.btn4 }}</li>
        <li @click.stop="mostrarInfo(inicio.btn5)">{{ inicio.btn5 }}</li>
        <li @click.stop="mostrarInfo(inicio.btn6)">{{ inicio.btn6 }}</li>
      </ul>
    </nav>
  </header>
  <section>
    <section id="banner">
      <h1 class="tituloBanner" :class="colorTxtBanner">{{ banner.title }}</h1>
      <p class="parrafoBanner" :class="colorTxtBanner">{{ banner.subTitle }}</p>
      <!-- Botones de la seccion Banner -->
    </section>
    <section id="registerForm" style="padding: 15vh; display: flex">
      <form
        style="
          border: solid 1px black;
          border-radius: 12px;
          width: fit-content;
          padding: 25px;
        "
        action=""
      >
        <h1>Registro</h1>
        <p>Nombre escrito: {{ nombreRegistro }}</p>
        Nombre:
        <input
          type="text"
          name=""
          id=""
          v-model="nombreRegistro"
          maxlength="10"
        /><br /><br />
        Sexo:
        <label for="male">Masculino</label>
        <input
          type="radio"
          name="sexo"
          :value="male"
          v-model="sexoSeleccionado"
          id="male"
        />
        <label for="female">Femenino</label>
        <input
          type="radio"
          name="sexo"
          :value="female"
          v-model="sexoSeleccionado"
          id="female"
        /><br /><br />
        <p>
          Preferencias seleccionadas:
          <span v-if="prefers.length > 0">{{ prefers }}</span>
        </p>
        Preferencias:
        <input
          type="checkbox"
          name="a"
          id="pa"
          value="Arte"
          v-model="prefers"
        />
        <label for="pa">Arte</label>
        <input
          type="checkbox"
          name="c"
          id="pc"
          value="Ciencia"
          v-model="prefers"
        />
        <label for="pc">Ciencia</label><br /><br />
      </form>
      <div style="display: flex; flex-direction: column">
        <div id="malex" v-if="sexoSeleccionado === male">Masculino</div>
        <template v-if="sexoSeleccionado === female">
          <p>Femenino</p>
          <p>Mas complicado</p>
        </template>
        <div id="science" v-if="prefers.includes('Ciencia')">Ciencia</div>
      </div>
    </section>
    <hr />
    <!-- Clase 3 Uso de v-for -->
    <section class="px-5">
      <h2>Usuarios</h2>
      <div
        class="row flex-row p-5 gap-3 justify-content-center"
        style="width: 100vw"
      >
        <template v-for="(user, idx) in usuarios" :key="user.id">
          <div class="card col-sm-3 mb-3 mb-sm-0">
            <div class="card-body">
              <h5 class="card-title" contenteditable="true">
                <b>{{ idx + 1 }}</b> - {{ user.name }}
              </h5>
              <p class="card-text">
                {{ user.company.bs }} -
                <span> >{{ user.company.catchPhrase }} </span> -
                <strong>{{ user.company.name }}</strong>
              </p>
              <a href="#" class="btn btn-primary">{{ user.phone }}</a>
            </div>
          </div>
        </template>
      </div>
    </section>
    <hr />
    <!-- Seccion para ejemplificar las computadas -->
    <button
      @click="
        dejar = !dejar;
        console.log(dejar);
      "
    >
      Suichar Computed
    </button>
    <Computed v-if="dejar" /><br />
    <hr />
    <input
      type="text"
      :ref="
        (el) => {
          inputId = el;
        }
      "
    />
    <button @click="cambiarID">Cambiar ID</button>
    <p class="text-danger">{{ mensajeDesdeWatch }}</p>
    <Watch :album-id="albumId" @mensajeParaPapa="(e) => {
      console.log(e);
      if (e != '') {
        mensajeDesdeWatch = e;
      }else{
        mensajeDesdeWatch = 'No se ha recibido mensaje desde Watch Component'
      }
    }">
      <template v-if="false">
        {{ algoParaSlot }} 
      </template> 
    </Watch>
  </section>
</template>

<style scoped>
header {
  background-image: linear-gradient(
    to bottom,
    #ffffff30,
    #ebebeb47,
    #d7d7d74a,
    #c4c4c441,
    #b1b1b11a
  );
  height: 70px;
  width: 100vw;
  padding: 0 2%;
  position: fixed;
  top: 0;
  z-index: 100;
}

#navHeader {
  width: 60vw;
}

#linksNav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  list-style: none;
}

.textoNegrita {
  font-weight: bold;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

/**Estilos del main */

/**Estilos del banner */
#banner {
  background-image: url("https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiXxN_42vXeZdwTL8NitxpeHe3MpgTKOKYAOShXZpFVw3E7T9MFc-7kRZsPrv8KgUgBLZPxQeXreDjnhRka9Qqpt5eZYSvcRlnh0HHp2Std2PwyxNFETDbPGII2o5vEp11tg5UbFxdylhjIwFKGv398jIdqp4LitvgYPTwiHgJNEAM1Ir2laveB6tVeNw/w640-h360/one-piece-1675092909888.jpg");
  background-size: 100% 100%;
  background-repeat: no-repeat;
  background-position: center center;
  height: 100vh;
  position: relative;
  top: 0;
  z-index: -5;
  width: 98.7vw;
  display: flex;
  flex-direction: column;
  /* justify-content: space-around;s */
  padding: 20vh 3vh;
}

.colorTxtBanner {
  color: #ffffff !important;
  font-size: 3.5em;
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
