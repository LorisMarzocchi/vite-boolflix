<script>

export default {
    name: "AppCard",
    data() {
        return {
            vote_Average: Math.round(this.vote_average / 2),
        }
    },

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
    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <img :src="this.poster_path ? `https://image.tmdb.org/t/p/w500${this.poster_path}` : 'immaginw dw'" alt="">
            </div>
            <div class="flip-card-back">
                Voto: {{ vote_Average }}
                <h3>Titolo: {{ title }}</h3>
                <h3>Titolo Originale: {{ original_title }}</h3>
                <h3>Lingua: {{ original_language }} </h3>
                <div class="vote">
                    Voto:
                    <ul class="icon">
                        <li v-for="i in 5" :key="i">
                            <font-awesome-icon :icon="i <= vote_Average ? ['fas', 'star'] : ['far', 'star']" />
                        </li>
                    </ul>
                </div>
                <h3>Actor</h3>
                <ul>
                    <li></li>
                    <!-- https://api.themoviedb.org/3/movie/165/credits?api_key=e99307154c6dfb0b4750f6603256716d& -->
                </ul>
            </div>
        </div>
    </div>
</template>



<style lang="scss" scoped>
.flip-card {
    background-color: transparent;
    width: calc((100% / 4) - 40px);
    height: 650px;
    margin: 20px;
    perspective: 1000px;
}

img {
    height: 100%;
    width: 100%;
}

.flip-card-inner {
    position: relative;
    width: 100%;
    height: 100%;
    text-align: center;
    transition: transform 0.6s;
    transform-style: preserve-3d;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}

.far {
    color: white;
}

.fas {
    color: white;

}

.flip-card:hover .flip-card-inner {
    transform: rotateY(180deg);
}

.vote {
    height: 5rem;
    width: 100%;
    display: flex;
}

.icon {
    display: flex;
    list-style: none;
}

i {
    font-size: 1rem;
    color: white;
}

.flip-card-front,
.flip-card-back {
    position: absolute;
    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}

h3 {
    padding-inline: 10px;
    margin-top: 4rem;
}

.flip-card-front {
    background-color: #bbb;
    color: black;
}

.flip-card-back {
    background-color: black;
    color: white;
    transform: rotateY(180deg);
}
</style>