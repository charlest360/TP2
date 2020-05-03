<template>
  <div class="page">
  
     <div class="home">
        <h1 v-bind:class='{ hidden: isClicked}'>Welcome to Our Movie Database!</h1>
        <span class="error in Home.vue :">{{error}}</span>
        
        <span class="static" v-bind:class='{ hidden: isClicked}' >Search a movie by keyword: <input v-model="filterName" /></span> 
        
        <button  class="static" v-bind:class='{ hidden: isClicked}'  @click="setIsClicked"> Rechercher</button>
        
        <button  class="static" v-bind:class='{ hidden: isClicked ==false }' @click="setIsClicked"> Back</button>
      
        <div class="movieData">
          <section class="static" v-bind:class='{ hidden: isClicked == false }' >
            <film-list :keyword="filterName" :clicked="isClicked" />
          </section>

        <section class="static" v-bind:class='{ hidden: shouldClose ==true }'>
          <film-suggestion-list :keyword="filterName" />
        </section>
      
        <section class="static" v-bind:class='{ hidden: isClicked}' >
          <home-movies-list :filmsData=filmsData />
        </section>
      </div>
      
    </div>
  </div>
 
</template>

<script>
import HomeMoviesList from '@/components/HomeMoviesList.vue'
import FilmService from '@/services/FilmService.js';
import FilmList from '@/components/FilmList.vue';
import FilmSuggestionList from '@/components/FilmSuggestionList.vue';
export default {
  name: 'Home',
  components: {
    HomeMoviesList,
    FilmList,
    FilmSuggestionList
  },
  data() {
    return {
      filmsData: null,
      error: null,
      filterName : '',
      isClicked : false
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

    
   
  },
  methods: {
    setIsClicked(){
      if(this.isClicked ==true) {
        this.isClicked = false;
      }
      else {
        this.isClicked = true;
      }
    }
  },
  computed: {
    shouldClose() {
      if(this.isClicked ==true || this.filterName.length < 3) {
        return true;
      } 
      else {
        return false;
      }
    }
  },
  
}
</script>

<style scoped>
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