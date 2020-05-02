<template>
    <div class="filmDetails">
        <section v-if="loading">
            <h2>Chargement des films...</h2>
        </section>
        <section v-else>
            <span class="error in filmDetails.vue :">{{error}}</span>
            <span class="title"> {{this.filmInfos.title}} </span>
            <span class=""></span>
            <span class=""></span>
            <span class=""></span>
            <span class=""></span>
        </section>
        
    </div>
</template>

<script>
import FilmService from '@/services/FilmService.js';
    export default {
        props: {
            filmId: {
                type: Number,
                required: true
            },
        },
        data() {
            return {
                error : null,
                loading : false,
                filmData: null
            }
        },
        created () {
            this.loading =true;
            FilmService.getFilmById(this.filmId)
            .then(response => {
            this.filmData = response.data;
            })
            .catch(error => {
            this.error = error;
            })
            .finally(() => this.loading =false);
            
            
            

        },
        computed: {
            filmInfos() {
                return this.filmData.film;
            },
            nbOfCritics() {
                return this.filmData.critic.length; 
            },
            criticsAverage(){
                let rating = 0;
                if (this.nbOfCritics > 0) {
                    for (let critic of this.filmData.critic)  {
                         rating += critic.score;
                    }
                    return (rating/this.nbOfCritics);
                }
                return rating;
            }
        },
        
        /*methods: {
            setFilmInfos() {
                this.filmInfos = this.filmData.film;
            },
            setNbOfCritics() {
                this.nbOfCritics = this.filmData.critic.length; 
            },
            setCriticAverage() {
                let rating = 0;
                if (this.nbOfCritics > 0) {
                    for (let critic of this.filmData.critic)  {
                         rating += critic.score;
                    }
                     this.criticsAverage =  (rating/this.nbOfCritics);
                }
               
            }

        },*/

    }
</script>

<style lang="scss" scoped>

</style>