<template>
  <div class="container">
    <h1 class="logo">
      <span>c</span>
      <span>a</span>
      <span>a</span>
      <span>a</span>
      <span>g</span>
      <span>e</span>
    </h1>
    <h2 class="page-title">{{ prompt }}</h2>
    <p v-if="error">{{ error }}</p>

    <ul class="covers list--unstyled" v-if="films">

      <li v-for="(film, index) in films" 
        v-if="index < 12"
        v-bind:index="index"
        v-bind:class="{ 'is-correct': film.isCorrect, 'is-wrong': film.isWrong }">
        <div class="cover-img" v-if="film.backdrop_path">
          <img v-bind:src="getBackdrop(index)">
          <div class="film-title">{{ film.title }}</div>
        </div>
        <form @submit.prevent="submitAnswer(index)" v-bind:data-index="index">
          <input type="text" placeholder="Type film here..." v-model.trim="filmInputs[index]" v-bind:disabled="film.isCorrect">
          <button type="submit" class="btn btn--check btn--block" v-bind:disabled="film.isCorrect">Check</button>
        </form>
      </li>

    </ul>
  </div>
</template>

<script>

export default {
  name: 'home',
  data () {
    return {
      title: 'caaage',
      prompt: 'Guess the film titles! They all star Nicholas Cage...',
      films: '',
      error: '',
      imgBaseUrl: 'http://image.tmdb.org/t/p/w780/',
      filmInputs: {},
      isCorrect: false,
      isWrong: false
    }
  },
  methods: {
    fetchFilms () {
      this.$http.get('https://api.themoviedb.org/3/discover/movie?with_cast=2963&api_key=9b1a22b01884b889ed192ba89db7edeb&language=en-US&page=1')
        .then(response => {
          this.films = response.data.results
        }, response => {
          this.error = response.statusText
        })
    },

    getBackdrop (index) {
      return this.imgBaseUrl + this.films[index].backdrop_path
    },

    submitAnswer (index) {
      let title = this.films[index].title.toLowerCase().replace(/[. /,:;-]+/g, '')
      let input = this.filmInputs[index].toLowerCase().replace(/[. /,:;-]+/g, '')

      if (title === input) {
        // Add isCorrect property to film object
        this.$set(this.films[index], 'isCorrect', true)
        this.$set(this.films[index], 'isWrong', false)
      } else {
        this.$set(this.films[index], 'isWrong', true)
      }
    }
  },

  mounted () {
    this.fetchFilms()
  }
}

</script>

<style lang="scss">
   @import 'app.scss'
</style>
