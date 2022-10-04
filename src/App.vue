<template>
  <div id="app">
    <div>
      <input type="text" v-model="query"/> <button @click="search">Cerca</button>
    </div>
    <div class="container">
      <h2>Movies</h2>
      <MovieCardComponent v-for="movie in movies" :key="movie.id" :movie="movie"  />
      <h2>TV Series</h2>
      <TvSerieCardComponent v-for="tvSerie in tvSeries" :key="tvSerie.id" :tv="tvSerie"  />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { apiKey } from '@/env'

import MovieCardComponent from '@/components/MovieCardComponent.vue'
import TvSerieCardComponent from '@/components/TvSerieCardComponent.vue'

export default {
  name: 'App',
  data(){
    return {
      query: '',
      movies: [],
      tvSeries: [],
      apiUrl: 'https://api.themoviedb.org/3/'
    }
  },
  methods:{
    search(){
      this.queryApi(this.query);
    },
    queryApi(textToSearch){
      const params = `?api_key=${apiKey}&query=${textToSearch}&language=it-IT`

      axios.get(`${this.apiUrl}search/movie${params}`)
        .then((response)=>{
          this.movies = this.getDataFromApiResponse(response);  
        })
        .catch(error=> {
          console.log(error.message)
        });
      axios.get(`${this.apiUrl}search/tv${params}`)
        .then((response)=>{
           this.tvSeries = this.getDataFromApiResponse(response);  
        })
        .catch(error=> {
          console.log(error.message)
        });
    },
    getDataFromApiResponse(response){
      console.log(response);
      return response.status === 200? response.data.results : []    
    }
  },
  components:{
    MovieCardComponent,
    TvSerieCardComponent
  }
}
</script>

<style lang="scss">
@import '~bootstrap/scss/bootstrap';

</style>
