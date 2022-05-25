<template>
  <div>
    <div class="container mx-auto">
      <div class="flex flex-row flex-wrap py-4">
        <div class="sticky top-0 pt-0 pb-4 py-4 w-full">
          <NavBar />
        </div>
        <div role="main" class="w-full sm:w-full md:w-full pt-1 px-10">
          <div class="grid grid-cols-3 gap-6">
            <div
              class="col-span-2 bg-white rounded-lg border border-gray-200 shadow-md dark:bg-gray-800 dark:border-gray-700"
            >
              <img class="rounded-t-lg" :src="newsContent && newsContent.urlToImage" alt="" />

              <div class="p-5">
                <span
                  class="bg-gray-100 text-gray-800 text-xs font-medium inline-flex items-center px-2.5 py-0.5 rounded mr-2 dark:bg-gray-700 dark:text-gray-300"
                >
                  <svg
                    class="mr-1 w-3 h-3"
                    fill="currentColor"
                    viewBox="0 0 20 20"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-12a1 1 0 10-2 0v4a1 1 0 00.293.707l2.828 2.829a1 1 0 101.415-1.415L11 9.586V6z"
                      clip-rule="evenodd"
                    ></path>
                  </svg>
                  {{ convertDate }}
                </span>
                <a href="#">
                  <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
                    {{ newsContent && newsContent.title }}
                  </h5>
                </a>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                  {{ newsContent && newsContent.description }}
                </p>
                <ul class="my-7 space-y-5">
                  <li class="flex space-x-3">
                    <svg
                      class="flex-shrink-0 w-5 h-5 text-blue-600 dark:text-blue-500"
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <span
                      class="text-base font-normal leading-tight text-gray-500 dark:text-gray-400"
                      >Author: {{ newsContent && newsContent.author }}</span
                    >
                  </li>
                  <li class="flex space-x-3">
                    <svg
                      class="flex-shrink-0 w-5 h-5 text-blue-600 dark:text-blue-500"
                      fill="currentColor"
                      viewBox="0 0 20 20"
                      xmlns="http://www.w3.org/2000/svg"
                    >
                      <path
                        fill-rule="evenodd"
                        d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                        clip-rule="evenodd"
                      ></path>
                    </svg>
                    <span
                      class="text-base font-normal leading-tight text-gray-500 dark:text-gray-400"
                      >Source: {{ newsContent && newsContent.source.id }}</span
                    >
                  </li>
                </ul>
                <a
                  :href="newsContent && newsContent.url"
                  target="blank"
                  class="inline-flex items-center py-2 px-3 text-sm font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                >
                  Read more
                </a>
              </div>
            </div>
            <div class="col-span-1">
              <RecentlyViewed />
            </div>
          </div>
        </div>
      </div>
      <div>
        <FooterView />
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue';
import FooterView from '@/components/FooterView.vue';
import RecentlyViewed from '../components/RecentlyViewed.vue';

export default {
  name: 'NewsDetail',
  components: {
    NavBar,
    RecentlyViewed,
    FooterView,
  },
  mounted() {
    this.updateHistory();
  },
  methods: {
    updateHistory() {
      let historyList = localStorage.getItem('newsHistory');
      historyList = historyList ? historyList.split(',') : [];

      historyList.push(this.newsContent.title);
      localStorage.setItem('newsHistory', historyList.toString());
    },
  },
  data() {
    return {
      newsContent: JSON.parse(this.$route.params.newsContent),
    };
  },
  computed: {
    convertDate() {
      const date = new Date(this.newsContent.publishedAt);
      return `${date.getFullYear()}. ${date.getMonth() + 1 > 9 ? '' : '0'}${date.getMonth() + 1}. ${
        date.getDate() > 9 ? '' : '0'
      }${date.getDate()}`;
    },
  },
};
</script>

<style scoped></style>
