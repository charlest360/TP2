<template>
  <div class="page">
    tit
     <div class="home">
      <h1>Welcome to Our Movie Database!</h1>
      <span class="error in Home.vue :">{{error}}</span>
      <home-movies-list :filmsData=filmsData />
    </div>
  </div>
 
</template>

<script>
import HomeMoviesList from '@/components/HomeMoviesList.vue'
import FilmService from '@/services/FilmService.js';
export default {
  name: 'Home',
  components: {
    HomeMoviesList
  },
  data() {
    return {
      filmsData: null,
      error: null,
    }
  },
  created () {
    
    FilmService.getFilms()
      .then(response => {
        this.filmsData = response.data;
      })
      .catch(error => {
        this.error = error;
      });

    
   
  }
}
</script>

<style scoped>
  .page {
    width : 70%;
    margin:  auto;
    text-align: center;
  
  }
</style>