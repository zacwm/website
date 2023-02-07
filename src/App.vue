<script>
import MainBox from './components/MainBox.vue';
import About from './components/About.vue';
import Work from './components/Work.vue';

export default {
  data() {
    return {
      page: 'home',
    }
  },
  components: {
    MainBox,
    About,
    Work,
  },
  methods: {
    clicked(page) {
      this.page = page;
    }
  }
};
</script>

<template>
  <div class="parentbox">
    <MainBox
      @clicked="clicked"
      :page="page"
    />
    <div class="subpageParent" :class="{ 'fadeIn': page == 'about' }">
      <About />
    </div>
    <div class="subpageParent" :class="{ 'fadeIn': page == 'work' }">
      <Work />
    </div>
  </div>
</template>

<style scoped>
  .parentbox {
    display: block;
    height: 100vh;
    width: 100%;
    padding: 60px;
    overflow-y: auto; 
  }

  .subpageParent {
    display: none;
    opacity: 0;
  }

  .fadeIn {
    display: block;
    animation: fadeIn 0.5s ease-out;
    animation-fill-mode: forwards;
  }

  @keyframes fadeIn {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }

  @media screen and (max-width: 768px) {
    .parentbox {
      padding: 20px;
    }
  }
</style>