<template>
  <div class="HomeMovieList">
    <section v-if="loading">
            <h2>Chargement en cours...</h2>
    </section>
    <section v-else>
      <Film-Details :filmId="totalOfFilms" />
      <Film-Details :filmId="totalOfFilms-1" />
      <Film-Details :filmId="totalOfFilms-2" />
    </section>
    
    <ul class="films">
     
    </ul>
  </div>
</template>

<script>
import FilmDetails from '@/components/FilmDetails.vue';
export default {
  name: 'HelloWorld',
  components: {
    FilmDetails,
  },
  props: {
    filmsData: {
      type : Object,
      default : null
    }
  },
  computed: {
    totalOfFilms() {
      if (this.filmsData != null) {
        return this.filmsData.meta.total;
      }
       else{
         return 0;
       }
    },
    loading() {
      if(!this.totalOfFilms > 0 ) {
        return true;
      }
      else {
        return false;
      }
    }
  },
    

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
