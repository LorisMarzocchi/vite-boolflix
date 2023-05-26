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
        overview: String,
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
                .catch(() => {
                    this.actors = ['N/A'];
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
                <h2>Titolo: {{ title }}</h2>
                <h2>Titolo Originale: {{ original_title }}</h2>
                <lang-flag class="language" :iso="original_language" :squared="false" />
                <span class="lang-text">language: {{ original_language }}</span>
                <div class="vote">
                    Voto:
                    <ul class="icon">
                        <li v-for="i in 5" :key="i">
                            <font-awesome-icon style="color: #FFBF00"
                                :icon="i <= vote_Average ? ['fas', 'star'] : ['far', 'star']" />
                        </li>
                    </ul>
                </div>
                <div class="overview">
                    {{ overview }}

                </div>
                <h2>Actor</h2>
                <ul>
                    <li class="actor" v-for="actor in actors" :key="actor">{{ actor }}

                    </li>
                    <!-- https://api.themoviedb.org/3/movie/{id.movie}/credits?api_key=e99307154c6dfb0b4750f6603256716d& -->
                </ul>
            </div>
        </div>
    </div>
</template>



<style lang="scss" scoped>
.actor {
    font-size: 1.2rem;

}

.overview {
    height: 4rem;
    font-size: 1.2rem;
    padding-inline: 1rem;
    line-height: 1.3rem;
    overflow: hidden;
    text-overflow: ellipsis;

}

.language {
    margin-top: 2rem;
    margin-bottom: 2rem;
    font-size: 2rem;
}

.flag-icon-undefined {
    display: none;
}

.lang-text {
    margin-top: 2rem;
    display: none;
    font-size: 2rem;
}

.flag-icon-undefined+.lang-text {
    display: inline;
    color: white;

}

.flip-card {
    background-color: transparent;
    width: calc((100% / 3) - 40px);
    height: 750px;
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
    font-size: 1.5rem;
    margin-top: 2rem;
    padding-inline: 2rem;
    height: 5rem;
    display: flex;
}

.icon {
    display: flex;
    margin-inline: 1rem;
}

li {
    list-style: none;

}

i {
    margin: 1rem;
    font-size: 2rem;
    color: white;
}

.flip-card-back {

    overflow-y: auto;
}


.flip-card-front,
.flip-card-back {
    position: absolute;

    width: 100%;
    height: 100%;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
}

h2 {
    padding-inline: 10px;
    margin-top: 2rem;
    margin-bottom: 2rem;
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