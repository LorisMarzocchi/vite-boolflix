<script>
import axios from 'axios';
import LangFlag from 'vue-lang-code-flags';
export default {
    name: "AppCard",
    data() {
        return {
            vote_Average: Math.round(this.vote_average / 2),
            LangFlag,
            actors: [],
        }
    },

    props: {
        poster_path: String,
        title: String,
        original_title: String,
        original_language: String,
        vote_average: Number,
        id: Number,
    },
    created() {
        this.fetchActors();
    },
    methods: {

        fetchActors() {
            axios
                .get(`https://api.themoviedb.org/3/movie/${this.id}/credits`, {
                    params: {
                        api_key: '95f92b62827d48d27c5483a9415a484d',
                    },
                })
                .then((response) => {
                    const credits = response.data;
                    if (credits.cast && credits.cast.length >= 0) {
                        this.actors = credits.cast.slice(0, 5).map((actor) => actor.name);
                    } else {
                        this.actors = ['N/A'];
                    }
                })
                .catch((error) => {
                    if (error.response && error.response.status === 404) {
                        this.actors = ['N/A'];
                    } else {
                        console.log(error);

                    }
                });

        },
    },
};
</script>
<template>
    <div class="flip-card">
        <div class="flip-card-inner">
            <div class="flip-card-front">
                <img :src="this.poster_path ? `https://image.tmdb.org/t/p/w500${this.poster_path}` : 'http://via.placeholder.com/640x360'"
                    alt="">
            </div>
            <div class="flip-card-back">
                <h3>Titolo: {{ title }}</h3>
                <h3>Titolo Originale: {{ original_title }}</h3>
                <lang-flag :iso="original_language" :squared="false" />
                <span class="lang-text">{{ original_language }}</span>
                <div class="vote">
                    Voto:
                    <ul class="icon">
                        <li v-for="i in 5" :key="i">
                            <font-awesome-icon style="color: #FFBF00"
                                :icon="i <= vote_Average ? ['fas', 'star'] : ['far', 'star']" />
                        </li>
                    </ul>
                </div>
                <h3>Actor</h3>
                <ul>
                    <li v-for="actor in actors" :key="actor">{{ actor }}

                    </li>
                    <!-- https://api.themoviedb.org/3/movie/{id.movie}/credits?api_key=e99307154c6dfb0b4750f6603256716d& -->
                </ul>
            </div>
        </div>
    </div>
</template>



<style lang="scss" scoped>
.lang-icon-undefined {
    display: none;
}

.lang-text {
    display: none;
}

.lang-icon-undefined+.lang-text {
    display: inline;
}

.flip-card {
    background-color: transparent;
    width: calc((100% / 4) - 40px);
    height: 700px;
    padding: 20px;
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
}

li {
    list-style: none;

}

i {
    font-size: 2rem;
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