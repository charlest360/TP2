<template>
    <div>
        <div class="ratingStars">
            <section v-if="loading">
                <h2>Chargement en cours...</h2>
            </section>
            <section v-else>
                
                    <div v-if="nbOfRatings > 5">
                       <span> xp Rating : {{ratingAverage}} </span> 
                    </div>
                    <div v-else>
                         <span>Rating : pas assez dévaluations </span> 
                    </div>
            </section>
            

        </div>
    </div>
</template>

<script>
    export default {
        props: {
            nbOfRatings: {
                type: Number,
                required : true 
            },
            ratingAverage: {
                type : Number,
                required : true
            }
        },
        computed: {
            loading() {
                 if(this.ratingAverage == null ) {
                    return true;
                }
                 else {
                    return false;
                }
            },
            /*starsRating() {
                let stars = ['@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png'];
                
                if (this.nbOfRatings >= 5 ) {
                switch(true) {
                    case this.ratingAverage >= 98:
                        stars = ['@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png'];
                        break;
                    case this.ratingAverage >= 88:
                        stars = ['@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarHalf.png'];
                        break;
                    case this.ratingAverage >= 78:
                        stars = ['@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarEmpty.png'];
                        break;
                    case this.ratingAverage >= 68:
                        stars = ['@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarHalf.png','@/assets/StarEmpty.png'];
                        break;
                    case this.ratingAverage >= 58:
                        stars = ['@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png'];
                        break;
                    case this.ratingAverage >= 48:
                        stars = ['@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarHalf.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png'];
                        break;
                    case this.ratingAverage >= 38:
                        stars = ['@/assets/StarFull.png','@/assets/StarFull.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png'];
                        break;
                    case this.ratingAverage >= 28:
                        stars = ['@/assets/StarFull.png','@/assets/StarHalf.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png'];
                        break;
                    case this.ratingAverage >= 18:
                        stars = ['@/assets/StarFull.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png'];
                        break;
                    case this.ratingAverage >= 8:
                        stars = ['@/assets/StarHalf.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png','@/assets/StarEmpty.png'];
                        break;
                    default:
                    
                    } 
                }
                 return stars;
            }*/
        },
    }
</script>

<style lang="scss" scoped>

</style>