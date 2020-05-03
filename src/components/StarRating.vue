<template>
    <div>
        <div class="ratingStars">
            <section v-if="loading">
                <h2>Chargement en cours...</h2>
            </section>
            <section v-else>
                    <span></span>
                    <div v-if="nbOfRatings >= 5">
                       <span class="starRate">  Rating : <star-rating
                            
                            v-bind:increment="0.5"
                            v-bind:max-rating="5"
                            inactive-color="#dbdbdb"
                            active-color="#cc1166"
                            v-bind:star-size="40"
                            :rating="criticsAverage" 
                            :read-only="true"/> </span> 
                    </div>
                    <div v-else>
                         <span class="starRate">Rating : <star-rating
                            
                            v-bind:increment="0.5"
                            v-bind:max-rating="5"
                            inactive-color="#dbdbdb"
                            active-color="#cc1166"
                            v-bind:star-size="40"
                            :rating="0"
                            :read-only="true"
                             />  not enough reviews</span> 
                    </div>
            </section>
            

        </div>
    </div>
</template>

<script>
import StarRating from 'vue-star-rating';
    export default {
        components: {
            StarRating,
        },
        props: {
            nbOfRatings: {
                type: Number,
                required : true,
                default : null 
            },
            ratings: {
                type : Array,
                required : true
            }
        },
        data() {
            return {
                criticsAverage: null
            }
        },
        computed: {
            loading() {
                 if(this.ratings == null ) {
                    return true;
                }
                 else {
                    return false;
                }
            },
             
        },
        created () {
            this.calculateCriticsAverage();
        },
            watch: {
                ratings : function() {
                    this.calculateCriticsAverage();
                }
            },
            methods: {
                calculateCriticsAverage() {
                    if (this.nbOfRatings >= 5) {
                         var i;
                        for (i = 0; i < this.nbOfRatings; i++) {
                            this.criticsAverage+= parseFloat( this.ratings[i].score);
                        }
                        this.criticsAverage = Math.round(((this.criticsAverage/this.nbOfRatings)*100)/20*1) /100; //division par 20 pour ramener sur 5
                    }
                },
                   
                                        
        },
                                    
            
    }
</script>

<style scoped>
    .starRate{
        display: inline-block;
    }
</style>