<script>
import AppCard from "./AppCard.vue";
import { store } from "../store";
export default {
    data() {
        return {
            store,
        };
    },
    components: {
        AppCard,
    },
};
</script>

<template>
    <div class="containerCard">
        <div class="container">
            <AppCard class="card-character" v-for="cards in store.cardList" :key="cards.id" :poster_path="cards.poster_path"
                :title="cards.title" :original_title="cards.original_title" :original_language="cards.original_language"
                :vote_average="cards.vote_average" />
            <AppCard class="card-character" v-for="cards in store.seriesList" :key="cards.id"
                :poster_path="cards.poster_path" :title="cards.name" :original_title="cards.original_name"
                :original_language="cards.original_language" :vote_average="cards.vote_average" />

        </div>
    </div>
</template>

<style lang="scss" scoped>
.container {
    display: flex;
    flex-wrap: wrap;
}

.containerCard {
    padding: 20px;
    height: 100%;
    margin: auto;
    width: 80%;
    background-color: white;
}

.countCard {
    text-align: center;
    padding: 1rem;
    margin-inline: 10px;
    height: 3rem;
    color: white;

}
</style>