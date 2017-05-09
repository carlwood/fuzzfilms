<template>
  <div class="container">
    <h1 class="logo">{{ title }}</h1>
    <h2 class="page-title">{{ prompt }}</h2>
    <a href="#" class="btn btn--lg btn--primary" v-on:click="fetchFilms()">Generate quiz</a>
    <p v-if="error">{{ error }}</p>
    <ul class="covers list--unstyled" v-if="films">
      <li v-for="(film, index) in films">
        <div class="cover-img">
          <img v-bind:src="getCover(index)">
        </div>
        <!-- <p>{{ film.title }}</p> -->
        <input type="text" placeholder="Type film here...">
        <button type="submit" class="btn btn--check btn--block">Check</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      title: 'fuzzfilms',
      prompt: 'Can you name these popular films from their fuzzy film posters?',
      films: '',
      error: '',
      imgBaseUrl: 'http://image.tmdb.org/t/p/w500/'
    }
  },
  methods: {
    fetchFilms () {
      this.$http.get('https://api.themoviedb.org/3/movie/popular?api_key=9b1a22b01884b889ed192ba89db7edeb&language=en-US&page=1')
        .then(response => {
          this.films = response.data.results
          console.log(response.data.results)
        }, response => {
          this.error = response.statusText
        })
    },
    getCover (index) {
      return this.imgBaseUrl + this.films[index].poster_path
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

.covers {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-row-gap: 30px;
  grid-column-gap: 30px;
  margin-top: 60px;
}

@media (min-width: 680px) {
  .covers {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media (min-width: 920px) {
  .covers {
    grid-template-columns: repeat(4, 1fr);
  }
}

@media (min-width: 1120px) {
  .covers {
    grid-template-columns: repeat(5, 1fr);
  }
}

.cover-img {
  margin-bottom: 5px;
  position: relative;
}

.cover-img img {
  filter: blur(7px);
}

.list--unstyled {
  list-style: none;
  padding: 0;
}
</style>
