<template>
  <div class="container mx-auto">
    <div class="flex flex-row flex-wrap py-4">
      <div class="sticky top-0 p-4 w-full">
        <NavBar />
      </div>
      <div role="main" class="w-full sm:w-2/3 md:w-3/4 pt-1 px-2">
        <!-- content area -->
      </div>
    </div>
  </div>
</template>

<script>
import NavBar from '@/components/NavBar.vue';

export default {
  name: 'HomeView',
  components: {
    NavBar,
  },
};
</script>
