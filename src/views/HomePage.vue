<template>
  <div id="app">
    <div class="wrapper ">
      <div class="columns">
        <div class="columns col1">
      <label class="has-text-info is-size-5" for="year">Year:</label>
        <input class="input is-primary" id="year" type="text" v-model="year" placeholder="Movie Year..">
      </div>
      <div class="columns col1">
        <label class="has-text-info is-size-5" for="rating">Rate:</label>
        <input class="input is-primary" id="rating" type="text" v-model="rating" placeholder="Movie Ratings..">
      </div>
      <div class="columns ">
        <button class="button is-medium is-info is-rounded" @click="fetchYearRate()">Search</button>
      </div>
      </div>
    </div>
    <div class="container">
           <div class="card-list">
        <CardItem v-for="movie in movieList.results" :key="movie.id"
          :cardTitle="movie.title"
          :cardContent="movie.overview"
          :cardImage="movie.poster_path"
          :cardDate="movie.release_date"
          :cardSlug="movie.id"
          :cardRate="movie.vote_average"
        >
        </CardItem>
      </div>
    </div>
  </div>
</template>

<script>
import CardItem from '../components/CardItem.vue';
export default {
  name: 'HomePage',
  components: {
    CardItem,
  },
  data() {
    return {
      movieList: [],
      genreList:[],
      year:'',
      rating:'',
      
    }
  },
  methods : {
    fetchMovie() {
      fetch('https://api.themoviedb.org/3/discover/movie?api_key=00d481b5200bd907e259829dcc6c3357&language=en-US&sort_by=popularity.desc&page=1')
      .then(response => response.json())
      .then(data => {
        this.movieList = data;
        console.log(this.movieList);
      })
    },
    fetchGenre() {
      fetch('https://api.themoviedb.org/3/genre/movie/list?api_key=00d481b5200bd907e259829dcc6c3357')
      .then(response => response.json())
      .then(data => {
        this.genreList = data;
        console.log(this.genreList);
      })
    },
    fetchYearRate() {
      
       fetch('https://api.themoviedb.org/3/discover/movie?api_key=00d481b5200bd907e259829dcc6c3357&language=en-US&primary_release_year='+this.year+'&vote_average.gte='+this.rating+'&vote_average.lte='+this.rating+'&sort_by=vote_average.desc&page=1')
       .then(response => response.json())
       .then(data => {
         this.movieList = data;
         console.log(this.movieList);
       })
     }
  },
  mounted() {
    this.fetchMovie();

  }
}
</script>

<style>
body{
  background-color: rgb(253, 253, 253);
}
  .card-list {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 30px;
    padding-top: 60px;
    padding-bottom: 60px;
  }
  img {
    object-fit:  cover !important;
  }
  .columns{
    display: flex;
    align-items: center;
    justify-content: space-around;
    padding: 20px 15px 10px 15px;
    border-radius: 5px;
    background-color: white;
  }
  .columns:last-child {
    margin-bottom: -0.01rem;
}
  label{
    margin-right: 10px;
  }
  button{
    padding-bottom: 20px;
  }
  @media(max-width: 767px){
    .card-list {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 30px;
    padding:50px;
  }
  .columns{
  
    display: flex;
    flex-wrap: wrap;
    background-color: white;
    flex-direction: column;
    align-content: space-around;
  }
  .col1{
    display: flex;
    flex-wrap: nowrap;
    background-color: white;
    flex-direction: row;
    align-items: baseline;
}
  }
  @media(min-width: 768px)and(max-width: 1024px){
    .card-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    padding: 30px;
    
  }

  }
</style>
