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
        v-if="film.backdrop_path"
        v-bind:index="index"
        v-bind:class="{ correct: film.isCorrect }">
        <div class="cover-img">
          <img v-bind:src="getBackdrop(index)">
          <div class="film-title">{{ film.title }}</div>
        </div>
        <form @submit.prevent="submitAnswer" v-bind:data-index="index">
          <input type="text" placeholder="Type film here..." v-model="filmInput[index]" v-on:keyup.enter="submitAnswer">
          <button type="submit" class="btn btn--check btn--block">Check</button>
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
      filmInput: {},
      isCorrect: false
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

    submitAnswer (e) {
      // @todo: change. pressing <enter> breaks this
      const index = e.target.dataset.index

      let title = this.films[index].title.toUpperCase()
      let input = this.filmInput[index].toUpperCase()

      if (title === input) {
        // Add isCorrect property to film object
        this.$set(this.films[index], 'isCorrect', true)
      } else {
        this.isWrong = true
        return false
      }
    }
  },

  mounted () {
    this.fetchFilms()
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

.covers {
  display: grid;
  grid-row-gap: 30px;
  grid-column-gap: 30px;
}

.cover-img:after {
  content: 'Correct!';
  display: flex;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transition: transform 0.4s;
  transform: translateY(-100%);
  justify-content: center;
  align-items: center;
  background: rgba(0,0,0,0.8);
  color: #fff;
  z-index: 5;
}

.correct .cover-img:after {
  transform: translateY(0%);
}

.film-title {
  background: #000;
  color: #fff;
  position: absolute;
  bottom: 0;
  left: 0;
  padding: 0.5rem 1rem;
  transform: translateY(100%);
  text-align: center;
  transition: transform 0.4s 0.5s;
  z-index: 10;
  width: 100%;
}

.correct .film-title {
  transform: translateY(0%);
}

@media (min-width: 680px) {
  .covers {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1000px) {
  .covers {
    grid-template-columns: repeat(3, 1fr);
  }
}

.cover-img {
  margin-bottom: 5px;
  position: relative;
  overflow: hidden;
}

.list--unstyled {
  list-style: none;
  padding: 0;
}
</style>
