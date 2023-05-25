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
    display: flex;
    justify-content: center;
    gap: 1rem;
    padding: 1.5rem 0;
}
</style>