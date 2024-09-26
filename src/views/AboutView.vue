<script setup>
  import { reactive, ref } from "vue";
  const creator = reactive({
    name: "Eduardo",
    lastname: "Mejias"
  });
  const signature = ref("Vue JS");
  //Crear dos variables para controlar el placeholder de cada input
  let valuePlaceholder = reactive({
    name: "Ingresa el nombre",
    password: "Ingresa la contraseña"
  });
  let btnDisabled = ref(false);
  let btnStyle = reactive({
    background: 'red',
    color: 'white'
  });
  function chBtn() {
    let newColor = `rgba(${Math.round(Math.random()*255)}, ${Math.round(Math.random()*255)}, ${Math.round(Math.random()*255)}, 1)`
    btnStyle.background = newColor;
  }
</script>

<template>
  <div class="about">
    <h1>El creador es: <span>{{ creator.name }} {{ creator.lastname }}</span></h1>
    <h2>El cual es el profesor de: <span>{{ signature }}</span></h2>
    <form action="">
      <div>
        <label for="inputName">Name</label>
        <input id="inputName" type="text" v-bind:placeholder="valuePlaceholder.name">
      </div>
      <div>
        <label for="inputPassword">Password</label>
        <input id="inputPassword" type="password" :placeholder="valuePlaceholder.password">
      </div>
      <input id="btnForm" type="button" value="Login" :disabled="btnDisabled" :style="btnStyle" @click="chBtn()">
    </form>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
    flex-direction: column;
    h1 {
      color: var(--vt-c-black);
    }
    h2 span{
      color: hsla(160, 100%, 37%, 0.895);
    }
    form div{
      display: flex;
      flex-direction: column;
      margin: 1rem;
    }
  }
  #btnForm{
    font-size: 2.5em;
    padding: 12px;
    border: none;
    border-radius: 12px;
  }
}
</style>
