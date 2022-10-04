<template>
   <div class="card">
        <p>Title: {{movie.title}}</p> 
        <p>Original Title: {{movie.original_title}}</p> 
        <p>Vote: {{movie.vote_average}}</p> 
        <p>Language: 
            <FlagComponent :language="movie.original_language"/>
        </p> 
        <PosterComponent :alt="movie.title" :image="movie.poster_path"/>
    </div>
</template>

<script>

import FlagComponent from '@/components/FlagComponent.vue'
import PosterComponent from '@/components/PosterComponent.vue'
export default {
    name: 'MovieCardComponent',
    props: {
        movie: Object
    },
    components: {
        FlagComponent,
        PosterComponent
    }
}
</script>

<style lang="scss" scoped>
.card{
  border: 1px solid red;
  background-color: gainsboro;
  margin: 5px;
}

</style>