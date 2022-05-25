<template>
  <div class="container mx-auto">
    <div class="flex flex-row flex-wrap py-4">
      <div class="sticky top-0 p-4 w-full">
        <NavBar />
      </div>
      <div role="main" class="w-full sm:w-full md:w-full pt-1 px-10">
        <!-- content area -->
        <div class="grid gap-4 md:grid-cols-3 sm:grid-cols-1">
          <CardView />
          <CardView />
          <CardView />
          <CardView />
          <CardView />
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
import FooterView from '../components/FooterView.vue';

export default {
  name: 'HomeView',
  components: {
    NavBar,
    CardView,
    FooterView,
  },
};
</script>
