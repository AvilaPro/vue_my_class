<script setup>
    import { ref } from "vue";
    import { IconCardsHeart } from '@iconify-prerendered/vue-mdi';

    const users = ref([]);

    fetch("https://jsonplaceholder.typicode.com/users").
    then(response => response.json()).
    then(data => {
        users.value = data;
        console.log(users);
    }) 
</script>

<template>
    <h1 style="text-align: center;"><IconCardsHeart /> Users</h1>
    <section id="users">
        <template v-for="user in users" :key="user.id">
            <p>{{ user.name }}</p>
        </template>
    </section>
</template>

<style scoped>
    #users{
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 2em;
        width: fit-content;
        border: solid  3px #3cff26;
        border-radius: 1em;
        margin: 2em auto 0;
    }
</style>