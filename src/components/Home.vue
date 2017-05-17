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
          <input type="text" placeholder="Type film here..." v-model.trim="filmInput[index]" v-bind:disabled="film.isCorrect">
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
      filmInput: {},
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
      let title = this.films[index].title.toLowerCase().replace(/[. ,:-]+/g, '')
      let input = this.filmInput[index].toLowerCase().replace(/[. ,:-]+/g, '')

      if (title === input) {
        // Add isCorrect property to film object
        this.$set(this.films[index], 'isCorrect', true)
      } else {
        this.$set(this.films[index], 'isWrong', true)
        let that = this
        setTimeout(function () {
          that.$set(that.films[index], 'isWrong', false)
        }, 1800)
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

form {
  transition: 0.8s opacity ease 0.6s;
}

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
  transition: transform 0.4s 0.2s;
  transform: translateY(-100%);
  justify-content: center;
  align-items: center;
  background: rgba(88, 158, 83, 0.8);
  color: #fff;
  z-index: 5;
}

.is-correct .cover-img:after {
  transform: translateY(0%);
}

.is-correct form {
  opacity: 0.3;
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
  transition: transform 0.4s 0.7s;
  z-index: 10;
  width: 100%;
}

.is-correct .film-title {
  transform: translateY(0%);
}

.is-wrong input[type='text'] {
  border-color: red;
  animation: shake 0.82s cubic-bezier(.36,.07,.19,.97) both;
  transform: translate3d(0, 0, 0);
  outline: none;
}

@media (min-width: 720px) {
  .covers {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1100px) {
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

@keyframes shake {
  10%, 90% {
    transform: translate3d(-1px, 0, 0);
  }
  
  20%, 80% {
    transform: translate3d(2px, 0, 0);
  }

  30%, 50%, 70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%, 60% {
    transform: translate3d(4px, 0, 0);
  }
}
</style>
