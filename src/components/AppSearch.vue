<script>
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
    },
};
</script>

<template>
    <div class="search-bar">
        <img src="../assets/Screenshot 2023-05-26 131527.png" alt="">

        <div>
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