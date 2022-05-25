<template>
  <div class="container mx-auto">
    <div class="flex flex-row flex-wrap py-4">
      <div class="sticky top-0 pt-0 pb-4 py-4 w-full">
        <NavBar />
      </div>
      <div role="main" class="w-full sm:w-full md:w-full pt-1 px-10">
        <!-- content area -->
        <div class="grid gap-4 md:grid-cols-3 sm:grid-cols-1 mx-auto container">
          <div v-for="(news, index) in newsList" :key="index">
            <CardView :news="news" />
          </div>
        </div>
      </div>
    </div>
    <div>
      <FooterView />
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue';
import CardView from '@/components/CardView.vue';
import Axios from 'axios';
import FooterView from '../components/FooterView.vue';

export default {
  name: 'HomeView',
  data() {
    return {
      newsList: null,
    };
  },
  components: {
    NavBar,
    CardView,
    FooterView,
  },
  mounted() {
    this.getNewsList();
  },
  methods: {
    getNewsList() {
      Axios.get(
        `${process.env.VUE_APP_NEWS_API_BASE_URL}/top-headlines?country=us&apiKey=${process.env.VUE_APP_NEWS_API_KEY}`
      ).then((response) => {
        if (response.status === 200) {
          this.newsList = response.data && response.data.articles;
        }
      });
    },
  },
};
</script>
