<template>
  <div id="app">
    <div>
      <input type="text" v-model="query"/> <button @click="search" >CERCA</button>
    </div>
    <div class="container">
      <div class="card" v-for="movie in movies" :key="movie.id">
        <p>Title: {{movie.title}}</p> 
        <p>Original Title: {{movie.original_title}}</p> 
        <p>Vote: {{movie.vote_average}}</p>
        <p>language: {{movie.original_language}}</p>
        <p>Language: 
          <img class="flag" 
               :src="getFlag(movie.original_language)"
               :alt="movie.original_language"/>     
        </p>  
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
  },
  getFlag(country){
      switch(country){
        case 'en':{
          country = 'gb';
          break;
        }
        case 'ja':{
          country = 'jp'
          break;
        }
      }
      return `https://flagicons.lipis.dev/flags/1x1/${country}.svg`
    },
  }

}
</script>

<style lang="scss">
  @import '~bootstrap/scss/bootstrap';
.card {
  border: 1px solid red;
  margin: 5px;
}
.flag{
  max-width: 20px;
}
</style>
