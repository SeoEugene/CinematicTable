<template>
  <div class="movie__search">
    <h2>영화</h2>
    <h2 class="blind">검색하기</h2>
    <input type="search" v-model="searchTerm" @keyup.enter="search" placeholder="검색어를 입력해주세요!" />
    <button type="submit" @click="search">검색</button>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "MovieSearch",
  data() {
    return {
      searchTerm: "",
    };
  },
  methods: {
    async search() {
      try {
        console.log(this.searchTerm);
        const response = await axios.get(
          "https://api.themoviedb.org/3/search/movie",
          {
            params: {
              api_key: "ade9889e6c6c54cbf65cc7f38a2bec71",
              language: "ko-KR",
              query: this.searchTerm,
            },
          }
        );
        console.log(response);
        this.$emit("search-results", response.data.results);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>