<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="container">
      <div class="movie__inner">
        <MovieSearchSection @search-results="updateSearchResults" />
        <MovieTagSection @fetchMovies="fetchMovies" />
        <MovieContSection :movies="movies" />
      </div>
    </div>
  </main>
  <FooterSection />
</template>
<script>
import axios from "axios";

import HeaderSection from "@/components/section/HeaderSection.vue";
import MovieSearchSection from "@/components/contents/MovieSearch.vue";
import MovieTagSection from "@/components/contents/MovieTag.vue";
import MovieContSection from "@/components/contents/MovieCont.vue";
import FooterSection from "@/components/section/FooterSection.vue";

export default {
  name: "MoviehomePage",
  components: {
    HeaderSection,
    MovieSearchSection,
    MovieTagSection,
    MovieContSection,
    FooterSection,
  },
  data() {
    return {
      movies: [],
    };
  },
  computed: {},
  async mounted() {
    try {
      await this.fetchMovies("popular");
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async fetchMovies(category) {
      try {
        const response = await axios.get(
          `https://api.themoviedb.org/3/movie/${category}`,
          {
            params: {
              api_key: "ade9889e6c6c54cbf65cc7f38a2bec71",
              language: "ko-KR",
              page: "1",
            },
          }
        );
        this.movies = response.data.results;
      } catch (err) {
        console.log(err);
      }
    },
    updateSearchResults(results) {
      this.movies = results;
    },
  },
};
</script>