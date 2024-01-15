<template>
  <HeaderSection />
  <main id="main" role="main">
    <div class="container">
      <div class="search">
        <MovieSearch />
      </div>
      <div class="detail__inner">
        <div class="movie__thumb">
          <DetailIntro v-if="movieBasic" :movieBasic="movieBasic" />
        </div>
        <div class="movie__info">
          <DetailInfo v-if="movieInfo" :movieInfo="movieInfo" />
        </div>
        <div class="movie__star">
          <DetailCredits v-if="movieCredits" :movieCredits="movieCredits" />
        </div>
        <div class="movie__review">
          <DetailReview v-if="movieReview" :movieReview="movieReview" />
        </div>
      </div>
    </div>
  </main>
  <FooterSection />
</template>
<script>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";
import HeaderSection from "@/components/section/HeaderSection.vue";
import MovieSearch from "@/components/contents/MovieSearch.vue";
import DetailIntro from "@/components/detail/DetailIntro.vue";
import DetailInfo from "@/components/detail/DetailInfo.vue";
import DetailCredits from "@/components/detail/DetailCredits.vue";
import DetailReview from "@/components/detail/DetailReview.vue";
import FooterSection from "@/components/section/FooterSection.vue";

export default {
  name: "MovieDetailPage",
  components: {
    HeaderSection,
    MovieSearch,
    DetailIntro,
    DetailInfo,
    DetailCredits,
    DetailReview,
    FooterSection,
  },

  setup() {
    const movieBasic = ref(null);
    const movieInfo = ref(null);
    const movieCredits = ref(null);
    const movieReview = ref(null);

    const route = useRoute();

    onMounted(async () => {
      // get방식
      const movieId = route.params.movieId;
      // api키 값 가져오기 (.env)
      const apiKey = import.meta.env.VITE_API_KEY;
      // 언어 설정
      const language = "ko-KR";

      try {
        const resMovieBasic = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`
        );
        console.log(resMovieBasic.data);
        movieBasic.value = resMovieBasic.data;

        const resMovieInfo = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}?language=${language}&api_key=${apiKey}`
        );
        movieInfo.value = resMovieInfo.data;

        const resmovieCredits = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}/credits?language=${language}&api_key=${apiKey}`
        );
        console.log(resmovieCredits.data);
        movieCredits.value = resmovieCredits.data;

        const resMovieReview = await axios.get(
          `https://api.themoviedb.org/3/movie/${movieId}/reviews?language=${language}&api_key=${apiKey}`
        );
        console.log(resMovieReview.data);
        movieReview.value = resMovieReview.data;
      } catch (err) {
        console.log(err);
      }
    });

    return { movieBasic, movieInfo, movieCredits, movieReview };
  },
};
</script>