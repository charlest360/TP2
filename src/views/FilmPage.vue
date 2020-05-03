<template>
    <div>
        <section v-if="loading ==true">
            <span>Loading</span>
        </section>
        <section v-else>
            
            <span class="static" v-bind:class='{ hidden: isClicked}' >Search a movie by keyword: <input v-model="filterName" /></span> 
        
            <button  class="static" v-bind:class='{ hidden: isClicked}'  @click="setIsClicked"> Rechercher</button>
        
            <button  class="static" v-bind:class='{ hidden: isClicked ==false }' @click="setIsClicked"> Back</button>
            
            
            
                
                <section class="static" v-bind:class='{ hidden: isClicked == false }' >
                    <film-list :keyword="filterName" :clicked="isClicked" />
                 </section>

                <section class="static" v-bind:class='{ hidden: shouldClose ==true }'>
                    <film-suggestion-list :keyword="filterName" />
                </section>
                
                <section>
                    <ul class="static" v-bind:class='{ hidden: isClicked}' id="filmData">
                        <li id="filmId"> <h1>{{filmData.film.title}}</h1> </li>
                
                        <li id="filmImage"> 
                            <section v-if="filmData.film.image != null  && filmData.film.image.length >0 ">
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
                
         
        </section>
        
    </div>
</template>

<script>
import FilmSuggestionList from '@/components/FilmSuggestionList.vue';
import FilmList from '@/components/FilmList.vue';
import StarRating from '@/components/StarRating.vue';
import FilmService from '@/services/FilmService.js';
import FilmActors from '@/components/FilmActors.vue';
    export default {
        components: {
            StarRating,
            FilmActors,
            FilmSuggestionList,
            FilmList
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
                filterName : '',
                isClicked : false
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
            },
            shouldClose() {
                 if(this.isClicked ==true || this.filterName.length < 3) {
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
            },
            setIsClicked(){
                if(this.isClicked ==true) {
                    this.isClicked = false;
                }
                else {
                    this.isClicked = true;
                }
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

.hidden {
    display: none;
}

.page {
    width : 70%;
    margin:  auto;
    text-align: center;
  
  }
  .hidden {
    display: none;
  }
  .movieData {

    background-color: LightGray;
  }

</style>