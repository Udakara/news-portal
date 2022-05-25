<template>
  <div>
    <div>
      <div className="rounded-lg shadow-2xl flex flex-col mb-4 p-2 bg-white">
        <div className="flex w-full">
          <div className="flex border-none rounded w-full">
            <input
              type="text"
              className="py-2 w-full"
              placeholder="Search news ..."
              aria-label="search news"
              v-model="searchText"
              @input="getSearchedNewsList"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from 'axios';

export default {
  name: 'SearchBar',
  data() {
    return {
      searchText: '',
    };
  },
  methods: {
    getSearchedNewsList() {
      Axios.get(
        `${process.env.VUE_APP_NEWS_API_BASE_URL}/top-headlines?q=${this.searchText}&apiKey=${process.env.VUE_APP_NEWS_API_KEY}`
      ).then((response) => {
        if (response.status === 200) {
          this.$emit('searchNews', response.data && response.data.articles);
        }
      });
    },
  },
};
</script>

<style scoped></style>
