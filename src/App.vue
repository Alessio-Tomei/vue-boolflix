<template>
<div id="app">
  <Header @searchUp="getApiQuery" />
  <Main :resultList="reFreshList" />
  <Footer/>
</div>
</template>

<script>
import axios from "axios";

import Header from "./components/macro/Header.vue";
import Main from "./components/macro/Main.vue";
import Footer from "./components/macro/Footer.vue";

export default {
  name: 'App',
  data() {
    return {
      movieArray: [],
      tvArray: [],
      loading: true,
      apiQuery: '',
      lastResearch: '',
    }
  },
  components: {
    Header,
    Main,
    Footer
  },
  methods: {
    getApiQuery: function(inputSearch) {
      this.apiQuery = inputSearch;
      if (this.apiQuery != '' && this.apiQuery != this.lastResearch ) {
        this.lastResearch = this.apiQuery;
        this.getMovie();
        this.getTv();
      }
    },
    getMovie: function() {
      axios.get('https://api.themoviedb.org/3/search/movie',
      {
        params: {
          api_key: 'c10c56018934cd53f73f023139b0b540',
          query: this.apiQuery,
        }
      })
      .then(apiResponse => {
          this.movieArray = apiResponse.data.results;
          this.loading = false;
        })
      .catch(() => {
        console.log('error');
      });
    },
    getTv: function() {
      axios.get('https://api.themoviedb.org/3/search/tv',
      {
        params: {
          api_key: 'c10c56018934cd53f73f023139b0b540',
          query: this.apiQuery,
        }
      })
      .then(apiResponse => {
          this.tvArray = apiResponse.data.results;
          this.loading = false;
        })
      .catch(() => {
        console.log('error');
      });
    },
    getStarsNumber: function(floatNumber) {
      return Math.ceil(floatNumber / 2);
    }
  },
  computed: {
    restructuresMovie() {
      const movies = [];
      this.movieArray.forEach(element => {
        const movieObj = {
          title: element.title,
          originalTitle: element.original_title,
          language: element.original_language,
          vote: element.vote_average,
          type: 'Film',
          poster: element.poster_path,
          stars: this.getStarsNumber(element.vote_average),
          overview: element.overview,
          popularity: element.popularity,
          voteCount: element.vote_count,
        };
        movies.push(movieObj);
      });
      return movies;
    },
    restructuresTv() {
      const tvs = [];
      this.tvArray.forEach(element => {
        const tvObj = {
          title: element.name,
          originalTitle: element.original_name,
          language: element.original_language,
          vote: element.vote_average,
          type: 'Serie Tv',
          poster: element.poster_path,
          stars: this.getStarsNumber(element.vote_average),
          overview: element.overview,
          popularity: element.popularity,
          voteCount: element.vote_count,
        };
        tvs.push(tvObj);
      });
      return tvs;
    },
    reFreshList() {
      console.log('counter');
      return [...this.restructuresMovie, ...this.restructuresTv].sort(function compareFn(firstEl, secondEl) {return (secondEl.vote * secondEl.voteCount) - (firstEl.vote * firstEl.voteCount)});
    }
  }
}
</script>

<style lang="scss">
@import "./assets/style/globals.scss";

</style>
