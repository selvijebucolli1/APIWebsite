<template>
  <div id="app">
    <div class="container">
      <div class="card-list">
        <CardItem v-for="news in newsList.results" :key="news.id"
          :cardTitle="news.title"
          :cardContent="news.overview"
          :cardImage="news.poster_path"
          :cardDate="news.release_date"
          :cardSlug="news.id"
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
      newsList: []
    }
  },
  methods : {
    fetchNews() {
      fetch('https://api.themoviedb.org/3/discover/movie?api_key=2c64846a6ec05dd248b9e8f65bba966b&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        this.newsList = data;
        console.log(this.newsList);
      })
    }
  },
  mounted() {
    this.fetchNews();
  }
}
</script>

<style>
  .card-list {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    padding-top: 60px;
    padding-bottom: 60px;
  }
  img {
    object-fit:  cover !important;
  }
</style>
