<template>
  <div class="card">
  <router-link :to="'/single-news/'+ cardSlug" >
  <div class="card-image">
    <figure class="image is-4by3">
      <img :src="'https://image.tmdb.org/t/p/original'+cardImage" :alt="cardTitle">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-content">
        <p class="title is-5">{{cardTitle}}</p>
      </div>
    </div>

    <div class="content">
      <p class="title is-6"><img class="rateLogo" src="../assets/1828884.png"> {{cardRate}}</p>
      <time class="title is-6" datetime="2016-1-1">{{cardDate}}</time>
    </div>
  </div>
</router-link>
</div>
</template>

<script>
export default {
  name: 'CardItem',
  props: {
    cardTitle: String,
    cardContent: String,
    cardImage: String,
    cardDate: String,
    cardSlug: Number,
    cardRate: Number,
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.rateLogo{
  width: 15px;
  height: 15px;
}
.media-content{
      padding-bottom: 30px;
    }
</style>
