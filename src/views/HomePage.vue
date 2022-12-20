<template>
  <div id="app">
    <div class="wrapper ">
      <div class="columns">
        <div class="columns">
      <label class="has-text-grey-darker is-size-5" for="year">Year:</label>
        <input class="input is-primary" id="year" type="text" v-model="year" placeholder="Movie Year..">
      </div>
      <div class="columns">
        <label class="has-text-grey-darker is-size-5" for="rating">Rate:</label>
        <input class="input is-primary" id="rating" type="text" v-model="rating" placeholder="Movie ..">
      </div>
      <div class="columns ">
        <button class="button is-medium is-info is-rounded" @click="fetchYearRate()">Search</button>
      </div>
      </div>
    </div>
    <div class="container">
           <div class="card-list">
        <CardItem v-for="news in newsList.results" :key="news.id"
          :cardTitle="news.title"
          :cardContent="news.overview"
          :cardImage="news.poster_path"
          :cardDate="news.release_date"
          :cardSlug="news.id"
          :cardRate="news.vote_average"
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
    CardItem
  },
  data() {
    return {
      newsList: [],
      year:" ",
      rating:" "
      
    }
  },
  methods : {
    fetchNews() {
      fetch('https://api.themoviedb.org/3/discover/movie?api_key=00d481b5200bd907e259829dcc6c3357&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        this.newsList = data;
        console.log(this.newsList);
      })
    },
    fetchYearRate() {
      
       fetch('https://api.themoviedb.org/3/discover/movie?api_key=00d481b5200bd907e259829dcc6c3357&language=en-US&primary_release_year='+this.year+'&vote_average.gte='+this.rating+'&vote_average.lte='+this.rating+'&sort_by=vote_average.desc&page=1')
       .then(response => response.json())
       .then(data => {
         this.newsList = data;
       })
     }
  },
  mounted() {
    this.fetchNews();
  }
}
</script>

<style>
body{
  background-color: rgb(65, 145, 176);
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
</style>
