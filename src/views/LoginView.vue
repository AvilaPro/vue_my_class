<script setup>
    import { ref } from "vue";
    const userData = ref({
        username: '',
        password: '',
        email: '',
        phone: '',
        preferences: [],
        sex: 'male',
        city: ''
    });

    const userRegistered = ref(true);
    const recordar = ref(false);

    function alertEl(msg) {
        alert(msg);
    }
</script>

<template>
    <section v-if="userRegistered" id="login" @click.self="alertEl('click en el section')">
        <form action="" @submit.stop.prevent="alertEl('Submit - Prevenido')" autocomplete="off">
            <div>
                <label for="username">Username</label>
                <input @keyup.up="console.log('presionaste ALT')" type="text" name="username" id="username">
            </div>
            <div>
                <label for="password">Password</label>
                <input @keydown.ctrl="alertEl('no se permite copiar o pegar')" @click.right="alertEl('no se permite el menu contextual en el input')" type="text" name="password" id="password" @paste.prevent="alertEl('no se permite pegar')">
            </div>
            <input @click.stop="" type="submit" value="Start">
        </form>
        <button @click.stop="recordar = !recordar">Recordarme</button> <span v-show="recordar"><span>Te recordaré</span></span>
        <button @click.stop="userRegistered = false">Register</button>
    </section>
    <section v-else id="register">
        <button @click.stop="userRegistered = true">Login</button>
        <form @submit.prevent="" action="" method="get">
            <div>
                <label for="username">Username</label>
                <input v-model="userData.username" @keyup.up="console.log('presionaste ALT')" type="text" name="username" id="username">
            </div>
            <div>
                <label for="email">email</label>
                <input v-model="userData.email" @keyup.up="console.log('presionaste ALT')" type="email" name="email" id="email">
            </div>
            <div>
                <label for="phone">phone</label>
                <input v-model="userData.phone" @keyup.up="console.log('presionaste ALT')" type="text" name="phone" id="phone">
            </div>
            <div>
                <label for="password">password</label>
                <input v-model="userData.password" @keyup.up="console.log('presionaste ALT')" type="password" name="password" id="password">
            </div>
            <div>
                <p>Selecciona tus favoritos:</p>
                <span>
                    <input v-model="userData.preferences" type="checkbox" name="angular" id="chkangular" value="angular">
                    <label for="chkangular">Angular</label>
                </span>
                <span>
                    <input v-model="userData.preferences" type="checkbox" name="vue" id="chkvue" value="vue">
                    <label for="chkvue">Vue</label>
                </span>
                <span>
                    <input v-model="userData.preferences" type="checkbox" name="react" id="chkreact" value="react">
                    <label for="chkreact">React</label>
                </span>
            </div>
            <div>
                <p>Sexo:</p>
                <input v-model="userData.sex" type="radio" name="sexo" id="radioMale" value="male">
                <label for="radioMale">Male</label>
                <input v-model="userData.sex" type="radio" name="sexo" id="radioFemale" value="female">
                <label for="radiofemale">Female</label>
            </div>
            <div>
                <label for="city">City</label>
                <select v-model="userData.city" name="city" id="city" >
                    <option :value="{ city: ''}">Select your city</option>
                    <option :value="{city: 'bqto'}">Barquisimeto</option>
                    <option :value="{city: 'sanf'}">San Felipe</option>
                    <option :value="{city: 'acar'}">Acarigua</option>
                    <option :value="{city: 'elto'}">El Tocuyo</option>
                </select>
            </div>
            <input @click="console.log(userData)" type="submit" value="Register">
        </form>
        
    </section>
</template>

<style scoped>
    section{
        width: 100vw;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    form{
        display: flex;
        width: fit-content;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        padding: 2em;
        margin: 2em auto;
        border: solid hsla(160, 100%, 37%, 1) 2px;
        border-radius: 1em;
        > div{
            margin: 1em 0;
            > label{
                margin-right: 0.5em;
            }
        }
    }
</style>