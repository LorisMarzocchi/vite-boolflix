<script>
import axios from 'axios';
import { store } from '../store';

export default {
    data() {
        return {

            store,
        };
    },
    methods: {

        emitSearchEvent() {
            this.$emit('performSearch');
        },
        requestIdGenre() {
            axios
                .get('https://api.themoviedb.org/3/genre/movie/list', {
                    params: {
                        api_key: '95f92b62827d48d27c5483a9415a484d',

                    }
                })
                .then(response => (this.store.idGenres = response.data.genres));
        }
    },
    created() {
        this.requestIdGenre();
    },
};
</script>

<template>
    <div class="search-bar">
        <img src="../assets/Screenshot 2023-05-26 131527.png" alt="">

        <div>
            <select @change="requestIdGenre">
                <option>All genres</option>
                <option v-for="idGen in store.idGenres" :key="idGen.id">{{ idGen.name }}</option>

            </select>

            <input type="text" placeholder="Search character" v-model="store.value" @keyup.enter="emitSearchEvent" />

            <button @click="emitSearchEvent">Search</button>

        </div>

    </div>
</template>

<style lang="scss" scoped>
.search-bar {
    height: 100px;
    display: flex;
    justify-content: space-around;
    gap: 1rem;
    padding: 1.5rem 0;
    background-color: black;
}

button {
    margin-left: 2rem;
    font-size: 1.5rem;
    border-radius: 10px;
    height: 50px;
    padding: 10px;

}

input {
    font-size: 1.5rem;
    border-radius: 10px;
    height: 50px;
    padding: 10px;
}
</style>