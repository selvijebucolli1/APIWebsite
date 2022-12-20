<template>
    <div id="app">
      <div class="container">
        <label for="year">Year</label>
        <input id="year" type="text" v-model="year" placeholder="Movie Year..">
        <label for="rating">Rate</label>
        <input id="rating" type="text" v-model="rating" placeholder="Movie ..">

        <button @click="fetchNews()">Search</button>

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
        rating:" ",
        year:" "
      }
    },
    methods : {
      fetchNews() {
        fetch('https://api.themoviedb.org/3/discover/movie?api_key=2c64846a6ec05dd248b9e8f65bba966b&language=en-US&year=' +this.year+'&page=1')
        .then(response => response.json())
        .then(data => {
          this.newsList = data;
        })
      }
    },
  }
  </script>
  
  <style>
  body{
    background-color: rgb(78, 168, 204);
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
  </style>
  