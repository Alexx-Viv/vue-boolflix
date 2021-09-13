<template>
  <section>
    <div>
      <input type="text" v-model="search" />
      <button type="button" @click="searchMovie()">
        Search
      </button>
    </div>
    <h2>Movie</h2>
    <div v-for="(movie, index) in movieList[0]" :key="index">
      <ul>
        <li>
          <img :src="`${posterBaseUrl}${movie.poster_path}`" alt="" />
        </li>
        <li>
          Title: <strong>{{ movie.title }}</strong>
        </li>
        <li>
          Original Title: <strong>{{ movie.original_title }}</strong>
        </li>
        <li>
          Original Language:
          <span v-if="searchFlag(movie.original_language)"
            ><img :src="srcFlag" width="50px" height="auto" alt=""
          /></span>

          <span v-else>{{ movie.original_language }}</span>
        </li>
        <li>
          Movie Average Vote:
          <strong>{{ averageVote(movie.vote_average) }}</strong>
        </li>
      </ul>
    </div>
    <h2>Series</h2>
    <div v-for="(series, index) in seriesList[0]" :key="index">
      <ul>
        <li>
          <img :src="`${posterBaseUrl}${movie.poster_path}`" alt="" />
        </li>
        <li>
          Title: <strong>{{ series.name }}</strong>
        </li>
        <li>
          Original Title: <strong>{{ series.original_name }}</strong>
        </li>
        <li>
          Original Language:
          <span v-if="searchFlag(series.original_language)"
            ><img :src="srcFlag" width="50px" height="auto" alt=""
          /></span>
          <span v-else>{{ series.original_language }}</span>
        </li>
        <li>
          Series Average Vote: <strong>{{ series.vote_average }}</strong>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data() {
    return {
      movieList: [],
      seriesList: [],
      search: '',
      searchLinkMovie: '',
      searchLinkSeries: '',
      flagList: ['it', 'en'],
      srcFlag: '',
      posterBaseUrl: 'https://image.tmdb.org/t/p/w342/',
    };
  },
  methods: {
    searchMovie() {
      this.movieList = [];
      this.seriesList = [];
      this.searchLinkMovie =
        'https://api.themoviedb.org/3/search/movie?api_key=4f27c01416f06baf9422adda6e42746d&query=' +
        this.search;
      this.searchLinkSeries =
        'https://api.themoviedb.org/3/search/tv?api_key=4f27c01416f06baf9422adda6e42746d&query=' +
        this.search;

      axios.get(this.searchLinkMovie).then((res) => {
        this.movieList.push(res.data.results);
      });
      axios.get(this.searchLinkSeries).then((res) => {
        this.seriesList.push(res.data.results);
      });
      console.log(this.seriesList);
      console.log(this.movieList[0]);
      this.search = '';
      this.searchLinkMovie = '';
      this.searchLinkSeries = '';
    },
    searchFlag(language) {
      if (this.flagList.includes(language)) {
        this.srcFlag = require('../assets/img/' + language + '.png');
        console.log(this.srcFlag);
        return true;
      } else {
        return false;
      }
    },
    averageVote(average) {
      return Math.ceil(average / 2);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
