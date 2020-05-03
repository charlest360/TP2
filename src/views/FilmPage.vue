<template>
    <div>
        <section v-if="loading ==true">
            <span>Loading</span>
        </section>
        <section v-else>
            <ul id="filmData">
                <li id="filmId"> <h1>{{filmData.film.title}}</h1> </li>
                
                <li id="filmImage"> <section v-if="filmData.film.image != null  && filmData.film.image.length >0 ">
                        <img :src="filmData.film.image" alt="une image" height="400" width="400">
                     </section>
            
                    <section v-else>
                        <img src="@/assets/noImage.png" alt="aucune image pour le film" height="400" width="400"> 
                     </section></li>
                     <li id="filmReview"><star-rating :nbOfRatings="filmData.critic.length" :ratings="filmData.critic" /> ({{filmData.critic.length}} reviews)</li>
                <li id="filmDescription"> Résumé : {{filmData.film.description}}</li>
                <li id="filmRanking"> Ranking : {{filmData.film.rating}}</li>
                <li id="filmLength"> Length : {{filmData.film.length}}</li>
                <li id="filmReleaseYear">Released in  {{filmData.film.release_year}}</li>
                <li> <film-actors :filmId="filmData.film.id"  /> </li>
            </ul>
         
        </section>
        
    </div>
</template>

<script>
import StarRating from '@/components/StarRating.vue';
import FilmService from '@/services/FilmService.js';
import FilmActors from '@/components/FilmActors.vue';
    export default {
        components: {
            StarRating,
            FilmActors
        },
        props: {
            id: {
                default: null,
                required: true
            },
        },
        data() {
            return {
                filmData: null,

            }
        },
        watch: {
            id: function() {
                this.getFilmInfos();
            }
        },
        created () {
            this.getFilmInfos();
        },
        computed: {
            loading() {
                if(this.filmData ==null) {
                    return true;
                } 
                else {
                    return false;
                }
            }
        },
        methods: {
            getFilmInfos() {
                FilmService.getFilmById(this.id)
                .then(response => {
                this.filmData = response.data;
                })
                .catch(error => {
                this.error = error;
                });
            }
        },
    }
</script>

<style scoped>
.filmData {
    width : 70%;
    margin: auto;
}
ul
{
    list-style-type:none;
    padding:0px;
    margin:0px;
}

#filmImage {
    width : 400px;
    height : 400px;
    background-color: lightgray;
    margin : auto;
}

</style>