<template>
  <article class="single-article">
    <div class="container has-background-white">
      <div class="column">
      <div class="column single-article__image">
        <img :src="'https://image.tmdb.org/t/p/original'+articleImage" :alt="articleImage">
      </div>
      <div class="column">
        <p class="title is-5">{{articleTitle}}</p>
      <div class="single-article__content content">
        <div> {{articleContent }}</div>
    <div class="content">
      <p class="title is-6"><img class="rateLogo" src="../assets/1828884.png"> {{articleRate}}</p>
      <time class="title is-6" datetime="2016-1-1">{{articleDate}}</time>
    </div>
      </div>
    </div>
    </div>
  </div>
  </article>

</template>

<script>

export default {
  name: 'SingleMovie',
  data() {
    return {
      articleTitle: '',
      articleContent: '',
      articleImage: '',
      articleRate: '',
      articleDate: ''
    }
  },
  methods: {
    fetchSingleMovie(movieID) {
      fetch('https://api.themoviedb.org/3//movie/'+ movieID+'?api_key=00d481b5200bd907e259829dcc6c3357&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        console.log(data);
        this.articleTitle = data.title,
        this.articleContent = data.overview;
        this.articleImage = data.poster_path;
        this.articleRate = data.vote_average;
        this.articleDate = data.release_date;
      })
    }
  },
  mounted() {
    this.fetchSingleMovie(this.$route.params.id);
  }
}
</script>

<style>
.single-article {
  padding-top: 60px;
  padding-bottom: 60px;
  text-align: left;
}
.column{
  display: flex;
  align-items: center;
  justify-content: flex-start;
  flex-direction: row;
  flex-wrap: wrap;
 
}
.single-article__image{
  display: flex;
  justify-content: space-around;
  
}
.rateLogo{
  width: 15px;
  height: 15px;
}
img {
    width: 60%;
    height: 20%;
  }
</style>