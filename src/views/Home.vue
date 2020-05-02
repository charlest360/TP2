<template>
  <div class="home">
    <h1>home</h1>
    <span class="error in Home.vue :">{{error}}</span>
    <hello-world :filmsData=filmsData />
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
import FilmService from '@/services/FilmService.js';
export default {
  name: 'Home',
  components: {
    HelloWorld
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
