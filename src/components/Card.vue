<template>
  <div>
    <div class="container">
      <div class="row justify-content-between">
        <div
          class="col-2 d-flex justify-content-center flex-wrap mb-4 card"
          v-for="(movie, index) in movieList"
          :key="index"
        >
          <img
            :src="`${posterBaseUrl}${movie.poster_path}`"
            alt=""
            class="poster"
          />
          <ul>
            <li>
              Title: <strong>{{ movie.title || movie.name }}</strong>
            </li>
            <li>
              Original Title:
              <strong>{{ movie.original_title || movie.original_name }}</strong>
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
              <strong v-html="averageVote(movie.vote_average)"></strong>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Card',
  props: ['movieList'],
  data() {
    return {
      posterBaseUrl: 'https://image.tmdb.org/t/p/w342/',
      flagList: ['it', 'en'],
    };
  },
  methods: {
    averageVote(average) {
      average = Math.ceil(average / 2);
      let star = '';
      for (let i = 0; i <= average; i++) {
        star += '<i class="fas fa-star"></i>';
      }
      average = 4 - average;
      for (let i = 0; i < average; i++) {
        star += '<i class="far fa-star"></i>';
      }
      return star;
    },
    searchFlag(language) {
      if (this.flagList.includes(language)) {
        this.srcFlag = require('../assets/img/' + language + '.png');
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style>
ul {
  list-style: none;
  position: absolute;
  right: 0%;
  top: 0%;
  width: 100%;
  height: 100%;
  padding-top: 20px;
  color: white;
  background-color: black;
  opacity: 0;
}

ul:hover {
  opacity: 1;
}

.card {
  min-width: 342px;
  min-height: 513px;
  position: relative;
}
.poster {
  width: 100%;
  height: auto;
}
</style>
