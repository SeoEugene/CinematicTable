<template>
  <div class="movie__title">{{ movieInfo.title }}</div>
  <div class="movie__desc">{{ movieInfo.overview }}</div>
  <span>
    <h4>장르</h4>
    <span
      class="movie__genres"
      v-for="genres in movieInfo.genres"
      :key="genres.id"
    >
      {{ genres.name }},
    </span>
  </span>
  <div class="movie__runtime">
    <h4>상영시간</h4>
    {{ formattedRuntime }}
  </div>
  <div class="movie__launching">
    <h4>개봉일</h4>
    {{ movieInfo.release_date }}
  </div>
  <div class="production">
    <h4>제작사</h4>
    <ul>
      <li v-for="company in movieInfo.production_companies" :key="company.id">
        {{ company.name }}
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: {
    movieInfo: Object,
  },
  computed: {
    formattedRuntime() {
      if (this.movieInfo && this.movieInfo.runtime) {
        const totalMinutes = this.movieInfo.runtime;
        const hours = Math.floor(totalMinutes / 60);
        const minutes = totalMinutes % 60;
        return `${hours}시간 ${minutes}분`;
      } else {
        return "";
      }
    },
  },
};
</script>