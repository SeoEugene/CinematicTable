<template>
  <img
    :src="getPostPath(movieBasic.poster_path)"
    :alt="movieBasic.spoken_languages.title"
  />
  <!-- <img
    :src="getPostPath(movieBasic.backdrop_path)"
    :alt="movieBasic.spoken_languages.title"
  /> -->
</template>
<script>
export default {
  props: {
    movieBasic: Object,
  },
  methods: {
    getPostPath(posterPath) {
      return `https://image.tmdb.org/t/p/w500${posterPath}`;
    },
  },
};
</script>