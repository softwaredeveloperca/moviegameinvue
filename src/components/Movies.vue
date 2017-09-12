<template>
  <div><h1>Movies</h1>
  <button class="primary" @click="getMyMovies()">
  My Movies
</button>
<button class="primary" @click="getAvailableMovies()">
  Buy Movies
</button>
  	<q-slider infinite arrows dots actions class="text-white">
  <div v-for="movie in movies" slot="slide" class="bg-faded">
   <div class="bg-white text-dark single-movie">
   <h4 class="text-dark wrap container">{{movie.Name}}</h4>

    	<span :class="getRandomColorClass(movie.Title)" class="tag label text-white" v-for="cat in getMovieCategories(movie.MovieType)">{{cat}}</span>
    	<p class="text-faded"><br><i>access_time</i> {{movie.Duration}} mins</p>
    	<p><b>Actors</b>: {{movie.actor_1_name}}, {{movie.actor_2_name}}, {{movie.actor_3_name}}<br>
    	<b>Director</b>: {{movie.director_name}}<br>
    	<b>Content Rating</b>: {{movie.content_rating}}<br>
    	<b>Year</b>: {{movie.title_year}}</p>
    	<span class="label bg-dark text-white shadow-1">Rating: {{movie.imdb_score}}</span><br><br>
  </div>

    	
  
  </div>
  <span slot="action" v-if="isGameList()">Sell <i @click="sellMovie()">
    remove_shopping_cart
  </i></span>
  <span slot="action" v-if="isPlayerList()">Buy <i @click="buyMovie()">
    add_shopping_cart
  </i>
  </span>
</q-slider>
  </div>
</template>

<script>
export default {
  props: {
    movies: Array
  },
  data () {
    return {
      current_movie_list_type: 'player',
      current_movies: this.movies,
      current_categories: this.categories,
      color_classes: ['bg-primary', 'bg-secondary', 'bg-tertiary', 'bg-info', 'bg-positive', 'bg-negative', 'bg-warning', 'bg-dark', 'bg-faded']
    }
  },
  methods: {
    getMovies: function () {
      return this.movies
    },
    getMyMovies: function () {
      this.current_movie_list_type = 'player'
      this.$emit('getMyMovies', [])
    },
    getAvailableMovies: function () {
      console.log('get game movies')
      this.current_movie_list_type = 'game'
      this.$emit('getAvailableMovies', [])
    },
    getRandomColorClass: function () {
      return this.color_classes[Math.floor(Math.random() * this.color_classes.length)]
    },
    getMovieCategories: function (value) {
      return value.split('|')
    },
    isPlayerList: function () {
      if (this.current_movie_list_type === 'player') {
        return true
      }
    },
    isGameList: function () {
      if (this.current_movie_list_type === 'game') {
        return true
      }
    },
    buyMovie: function (movieId) {
      this.$emit('buyMovie', movieId)
    },
    sellMovie: function (movieId) {
      this.$emit('sellMovie', movieId)
    }
  }
}
</script>

<style>
.single-movie { padding: 15px; }
.container {
  display: flex; /* or inline-flex */
  flex-wrap: wrap
}
</style>
