<script>

export default {
    name: "AppCard",

    props: {
        poster_path: String,
        title: String,
        original_title: String,
        original_language: String,
        vote_average: Number,
    },
    methods: {


    },
}
</script>
<template>
    <div class="cards">
        <div>{{ 'https://image.tmdb.org/t/p/w500' + this.poster_path }}</div>
        <h3>Titolo: {{ title }}</h3>
        <h3>Titolo Originale: {{ original_title }}</h3>
        <h3>Lingua: {{ original_language }} </h3>
        <h3>Voto: {{ vote_average }}</h3>
    </div>
</template>



<style lang="scss" scoped>
.cards {
    display: flex;
    flex-direction: column;
    justify-content: center;
    border: 1px solid black;
    height: 100%;
    text-align: center;

    margin-inline: 10px;
    margin-bottom: 10px;
}

div {
    height: 500px;
    width: 500px;
    object-fit: contain;
}

h3 {
    font-size: 2rem;
    color: black;
    margin: 1rem;
}

p {
    margin: 1rem;
}
</style>