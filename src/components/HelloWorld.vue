<template>
  <section>
    <div>
      <input type="text" v-model="search" />
      <button type="button" @click="searchMovie()">
        Cerca
      </button>
    </div>

    <div v-for="(movie, index) in movieList[0]" :key="index">
      <ul>
        <li>
          Title: <strong>{{ movie.title }}</strong>
        </li>
        <li>
          Original Title: <strong>{{ movie.original_title }}</strong>
        </li>
        <li>
          Original Language: <strong>{{ movie.original_language }}</strong>
        </li>
        <li>
          Movie Average Vote: <strong>{{ movie.vote_average }}</strong>
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
      search: '',
      searchLink: '',
    };
  },
  methods: {
    searchMovie() {
      this.movieList = [];
      this.searchLink =
        'https://api.themoviedb.org/3/search/movie?api_key=4f27c01416f06baf9422adda6e42746d&query=' +
        this.search;
      console.log(this.searchLink);
      axios.get(this.searchLink).then((res) => {
        this.movieList.push(res.data.results);
      });
      this.search = '';
      this.searchLink = '';
    },
  },
  created() {},
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
