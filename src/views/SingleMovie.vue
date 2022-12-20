<template>
  <article class="single-article">
    <div class="container">
      <div class="single-article__image">
        <img :src="'https://image.tmdb.org/t/p/original'+articleImage" :alt="articleImage">
      </div>
      <div class="single-article__content content">
        <div> {{articleContent }}</div>
      </div>
    </div>
  </article>

</template>

<script>
export default {
  name: 'SingleMovie',
  data() {
    return {
      articleContent: '',
      articleImage: ''
    }
  },
  methods: {
    fetchSingleMovie(movieID) {
      fetch('https://api.themoviedb.org/3//movie/'+ movieID+'?api_key=00d481b5200bd907e259829dcc6c3357&language=en-US&page=1')
      .then(response => response.json())
      .then(data => {
        console.log(data);
        this.articleContent = data.overview;
        this.articleImage = data[0].poster_path;
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
</style>