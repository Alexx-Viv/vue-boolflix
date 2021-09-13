<template>
  <div id="app">
    <header>
      <div class="container h-100">
        <div class="row h-100">
          <div class="col-6 h-100 d-flex align-items-center">
            <h1 class="text-danger font-weight-bold text-uppercase">Booflix</h1>
          </div>
          <div
            class="col-6 h-100 d-flex align-items-center justify-content-end"
          >
            <Search
              placeholder="Cerca un film..."
              buttonText="cerca"
              @search="getMovies($event)"
            />
          </div>
        </div>
      </div>
    </header>
    <main>
      <h2 class="text-center" v-if="isMovies()">Movie</h2>
      <Card :movieList="movies" />
      <h2 class="text-center" v-if="isSeries()">Series</h2>
      <Card :movieList="series" />
    </main>
  </div>
</template>

<script>
import axios from 'axios';
import Search from './components/Search.vue';
import Card from './components/Card.vue';

export default {
  name: 'App',
  components: {
    Search,
    Card,
  },
  data() {
    return {
      movies: [],
      series: [],
      api: {
        key: '4f27c01416f06baf9422adda6e42746d',
        baseUri: 'https://api.themoviedb.org/3/',
        endPointMovie: 'search/movie',
        endPointSeries: 'search/tv',
      },
    };
  },
  methods: {
    getMovies(query) {
      if (!query) {
        this.movies = [];
        this.series = [];
      }
      console.log(query);
      const params = {
        params: {
          query,
          api_key: this.api.key,
        },
      };
      axios
        .get(`${this.api.baseUri}${this.api.endPointMovie}`, params)
        .then((res) => {
          this.movies = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
      axios
        .get(`${this.api.baseUri}${this.api.endPointSeries}`, params)
        .then((res) => {
          this.series = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    isMovies() {
      if (this.movies.length == 0) {
        return false;
      } else {
        return true;
      }
    },
    isSeries() {
      if (this.series.length == 0) {
        return false;
      } else {
        return true;
      }
    },
  },
};
</script>

<style lang="scss">
header {
  height: 10vh;
  background-color: #2c3e50;
}
main {
  min-height: 90vh;
  width: 100%;
  background-color: #9f9f9f;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
