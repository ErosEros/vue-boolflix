<template>
  <div id="app">
    <div>
      <input type="text" v-model="query"/> <button @click="search" >CERCA</button>
    </div>
    <div class="container">
      <div v-for="movie in movies" :key="movie.id">
        {{movie.title}}
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { apiKey } from './components/env';


export default {
  name: 'App',
  data(){
    return {
      query: '',
      movies: '',
    }
  },
  // mounted(){
  //   this.queryApi('ritorno al fut');
  // },
  methods: {
    search(){
      this.queryApi(this.query);
    },

    queryApi(textToSearch){
    axios.get(`https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&query=${textToSearch}&language=it-IT`)
    .then((response)=>{
      console.log(response);
      if (response.status === 200){
            this.movies = response.data.results;
          }       
    })
    .catch(error =>{
      console.log(error.message)
    })
  }

  }


}
</script>

<style lang="scss">
  @import '~bootstrap/scss/bootstrap';

</style>
