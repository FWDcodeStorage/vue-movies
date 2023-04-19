<template>
    <div class="movie-detail">
        <div class="title">
            <h3>{{ movie.Title }}</h3>
        </div>
        <div class="header">
            <div class="rating">
                <h3>{{ movie.imdbRating }}</h3>
            </div>
            <div class="year">
                <p>{{ movie.Year }}</p>
            </div>
            <div class="runtime">
                <p>{{ movie.Runtime }}</p>
            </div>
        </div>

        <div class="movie-poster">
            <img :src="movie.Poster" :alt="movie.Title" />
            <div class="type">
                {{ movie.Type }}
            </div>
        </div>

        <div class="genre">
            <p>{{ movie.Genre }}</p>
        </div>

        <div class="description">
            <p>{{ movie.Plot }}</p>
        </div>

        <div @click="toggleActive" :class="{'active': !active}" class="more-info">
            <h5>More info</h5>

            <div v-if="active" class="info-inner">
                <div><p>Released: <span>{{ movie.Released }}</span></p></div>
                <div><p>Director: <span>{{ movie.Director }}</span></p></div>
                <div><p>Writer: <span>{{ movie.Writer }}</span></p></div>
                <div><p>Language: <span>{{ movie.Language }}</span></p></div>
                <div><p>Awards: <span>{{ movie.Awards }}</span></p></div>
                <div><p>Actors: <span>{{ movie.Actors }}</span></p></div>
            </div>
        </div>
    </div>
</template>

<script>
import { onBeforeMount, ref } from "vue";
import { useRoute } from "vue-router";


export default {
    setup() {
        const route = useRoute();
        const movie = ref({});
        const active = ref(false);
       

        onBeforeMount(() => {
            fetch(
                `http://www.omdbapi.com/?apikey=${process.env.VUE_APP_API_KEY}&i=${route.params.id}&plot=full`
            )
                .then((res) => res.json())
                .then((data) => {
                    movie.value = data;
                });
        });

        const toggleActive = () => {
           active.value = !active.value;
        }

        return {
            movie, active, toggleActive
        };
    },
};
</script>

<style lang="scss">
.movie-detail {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin: 10px 0;
    // align-items: center;
    padding: 15px 5px;

    h3 {
        font-size: 1.3rem;
        letter-spacing: 0.05rem;
    }

    .header {
        display: flex;
        justify-content: flex-start;
        gap: 10px;
        padding: 10px 0;

        .year,
        .runtime,
        .rating {
            background-color: rgb(3, 193, 246);
            padding: 5px 15px;
            border-radius: 5px;
            font-weight: bold;
        }
    }

    .movie-poster {
        position: relative;
        display: block;

        img {
            display: block;
            max-width: 300px;
            max-height: 40vh;
            object-fit: cover;

            z-index: 0;
        }

        .type {
            position: absolute;
            padding: 5px 15px;
            background-color: rgb(3, 193, 246);
            color: #fff;
            top: 15px;
            left: 0;
            text-transform: capitalize;
        }
    }

    .genre {
        margin-top: 15px;
        width: fit-content;
        background-color: rgb(3, 193, 246);
        padding: 5px 15px;
        border-radius: 5px;
        font-weight: bold;
    }

    .description {
        width: 100%;
        padding: 15px 0;

        p {
            color: #b5b5b5;
        }
    }

    .active{
        margin-top: 15px;
        width: fit-content;
        background-color: rgb(3, 193, 246);
        padding: 5px 15px;
        border-radius: 5px;
        font-weight: bold;
    }

    .more-info{
        margin-top: 15px;
        width: fit-content;
        padding: 5px 15px;
        cursor: pointer;

        .info-inner{
            margin-top: 15px;
            margin-bottom: 15px;

            div{
                margin-bottom: 8px;

                p{
                font-size: 0.8rem;
                color: #b5b5b5;
            }
            }
        }
    }
}
</style>
