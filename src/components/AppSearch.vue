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


        <input type="text" placeholder="Search character" v-model="store.value" @keyup.enter="emitSearchEvent" />

        <button @click="emitSearchEvent">Search</button>

    </div>
</template>

<style lang="scss" scoped>
.search-bar {
    height: 100px;
    display: flex;
    justify-content: center;
    gap: 1rem;
    padding: 1.5rem 0;
}

input {
    border-radius: 10px;
    height: 50px;
    padding: 10px;
}
</style>