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
            <div class="container">

                <h1>FILM:</h1>

            <AppCard class="card-character" v-for="cards in store.cardList" :overview="cards.overview" :id="cards.id"
                    :key="cards.id" :poster_path="cards.poster_path" :title="cards.title"
                    :original_title="cards.original_title" :original_language="cards.original_language"
                    :vote_average="cards.vote_average" />
            </div>
            <div class="container">

                <h1>SERIE:</h1>
                <AppCard class="card-character" v-for="cards in store.seriesList" :overview="cards.overview" :key="cards.id"
                    :id="cards.id" :poster_path="cards.poster_path" :title="cards.name"
                    :original_title="cards.original_name" :original_language="cards.original_language"
                    :vote_average="cards.vote_average" />
            </div>
            <!-- <AppCard class="card-character" v-for="cards in store.creditsList" :key="cards.id" :id="cards.id"
                                                                                            :poster_path="cards.poster_path" :title="cards.name" :original_title="cards.original_name"
                                                                                            :original_language="cards.original_language" :vote_average="cards.vote_average" /> -->

        </div>
    </div>
</template>

<style lang="scss" scoped>
.container {
    display: flex;
    flex-wrap: wrap;
    width: 80%;
    margin: auto;
}

.containerCard {
    background-color: #434343;
    padding: 20px;
    height: 100%;
    margin: auto;

}

.countCard {
    text-align: center;
    padding: 1rem;
    margin-inline: 10px;
    height: 3rem;
    color: white;

}
</style>