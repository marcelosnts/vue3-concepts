<template>
    <div>
        <h1 v-bind:style="{ textDecoration }">Hello {{ name }}</h1>
        <input type="text" v-model="name">

        <br>

        <a :href="link">Treinamento VueJS</a>
    </div>
</template>

<script>
    export default {
        data: () => ({
            name: 'Marcelo',
            link: 'https://treinamento.vuejsbrasil.org',
            textDecoration: 'underline'
        })
    }
</script>