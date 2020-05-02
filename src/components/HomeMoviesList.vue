<template>
  <div class="HomeMovieList">
    <Film-Details :filmId="totalOfFilms" />
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
    }
  },
    

}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
