<template>
  <section class="movie__cont">
    <h2 class="blind">영화</h2>
    <div class="ranking">1 - 10</div>
    <div>
      <div
        class="movie play__icon"
        v-for="movie in firstTenMovies"
        :key="movie.id"
      >
        <a :href="'/detail/' + movie.id">
          <img :src="getMoviePosterUrl(movie.poster_path)" :alt="movie.title" />
        </a>
        <div class="title">{{ movie.title }}</div>
      </div>
    </div>

    <div class="ranking">11 - 20</div>
    <div>
      <div
        class="movie play__icon"
        v-for="movie in secondTenMovies"
        :key="movie.id"
      >
        <a :href="'/detail/' + movie.id">
          <img :src="getMoviePosterUrl(movie.poster_path)" :alt="movie.title" />
        </a>
        <div class="title">{{ movie.title }}</div>
      </div>
    </div>
  </section>
  <!-- movie__cont -->
</template>
<script>
import axios from "axios";

export default {
  name: "MovieCont",
  props: {
    movies: {
      type: Array,
      required: true,
    },
  },
  //   data() {
  //     return {
  //     //   movies: [],
  //     };
  //   },
  computed: {
    firstTenMovies() {
      return this.movies.slice(0, 10);
    },
    secondTenMovies() {
      return this.movies.slice(10, 20);
    },
  },
  //   async mounted() {
  //     try {
  //       const response = await axios.get(
  //         "https://api.themoviedb.org/3/movie/popular",
  //         {
  //           params: {
  //             api_key: "ade9889e6c6c54cbf65cc7f38a2bec71",
  //             language: "ko-KR",
  //             page: "1",
  //           },
  //         }
  //       );
  //       this.movies = response.data.results;
  //     } catch (err) {
  //       console.log(err);
  //     }
  //   },
  methods: {
    getMoviePosterUrl(posterPath) {
      if (posterPath) {
        return `https://image.tmdb.org/t/p/w500${posterPath}`;
      } else {
        return "../../assets/image/noneimg.png";
      }
    },
  },
};
</script>