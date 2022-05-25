<template>
  <div>
    <div className="bg-white shadow-lg rounded-lg p-8 pb-12 mb-8">
      <h3 className="text-xl mb-8 font-semibold border-b pb-4">Recently Viewed News</h3>
      <div class="grid grid-cols-1 divide-y">
        <span
          className="cursor-pointer block mt-2 mb-2"
          v-for="(news, index) in newsList"
          :key="index"
          >{{ news }}</span
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecentlyViewed',
  data() {
    return {
      newsList: null,
    };
  },
  mounted() {
    let historyList = localStorage.getItem('newsHistory');
    historyList = historyList ? historyList.split(',') : [];
    this.newsList = historyList;
  },
};
</script>

<style scoped></style>
