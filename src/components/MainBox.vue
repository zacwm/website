<script lang="ts">
import Links from './Links.vue';
import Socials from './Socials.vue';

export default {
  props: ['page'],
  data() {
    return {
      mouseX: 0,
      mouseY: 0,
      mainboxFadeUp: false,
      contentboxFadeUp: false,
      aftertextFadeUp: false,
    };
  },
  created() {
    document.addEventListener("mousemove", this.updateMousePosition);
    
    // Do fade in animation for elements
    this.$nextTick(function () {
      this.mainboxFadeUp = true;
      setTimeout(() => {
        this.contentboxFadeUp = true;
      }, 1500);
      setTimeout(() => {
        this.aftertextFadeUp = true;
      }, 2500);
    });
  },
  beforeDestroy() {
    document.removeEventListener("mousemove", this.updateMousePosition);
  },
  computed: {
    elementPosition() {
      if (!this.mouseY) console.dir(this.mouseY);
      return {
        top: this.mouseY * -0.15 + "px",
        left: this.mouseX * -0.15 + "px",
      };
    },
    randomBackgroundInt() {
      const backgroundPaths = [
        "/background1.jpg",
        "/background2.jpg",
        "/background3.jpg",
      ];
      const randomInt = Math.floor(Math.random() * backgroundPaths.length);
      return backgroundPaths[randomInt];
    }
  },
  methods: {
    updateMousePosition(event) {
      this.mouseX = event.clientX;
      this.mouseY = event.clientY;
    },
    clicked(page) {
      this.$emit("clicked", page);
    }
  },
  components: { Links, Socials }
}
</script>

<template>
  <div
    class="mainbox"
    :class="{
      'mainboxPageSelected': page !== 'home',
      'fadeInUp': mainboxFadeUp,
    }"
  >
    <div
      class="parallaxbox"
      v-bind:style="{
        'top': elementPosition.top,
        'left': elementPosition.left,
        'background-image': 'url(' + randomBackgroundInt + ')'
      }"
    ></div>
    <div class="blurbox">
      <div class="interactiveParent">
        <Links @clicked="clicked" :page="this.page" />
        <Socials />
      </div>
      <div
        class="contentbox"
        :class="{
          'fadeInUp': contentboxFadeUp,
          'fadeOut': page !== 'home',
        }"
      >
        <p>Hi,</p>
        <p>I'm Zachary</p>
        <p class="afterText" :class="{ 'fadeInUp': aftertextFadeUp }">A full stack developer from Brisbane, Australia</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .fadeInUp {
    animation: fadeInUp 1s ease-in-out;
  }

  .fadeOut {
    animation: fadeOut .3s ease-in-out;
  }

  @keyframes fadeInUp {
    0% {
      opacity: 0s;
      transform: translateY(20px);
    }
    100% {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @keyframes fadeOut {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

  .mainbox {
    position: relative;
    height: 100%;
    width: 100%;
    background-color: #444;
    border-radius: 40px;
    overflow: hidden;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.5);
    opacity: 0;
    animation-fill-mode: forwards;
    transition: height 1s ease;
  }

  .mainboxPageSelected {
    height: 100px;
  }

  .parallaxbox {
    position: absolute;
    top: -20%;
    left: -20%;
    height: 120vh;
    width: 120vw;
    min-height: 400px;
    /* add parallax effect to background */
    
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    transition: .5s ease-out;
    transition-property: top, left;
  }

  .blurbox {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    /* add blur to background */
    background-color: rgba(0, 0, 0, 0.5);
  }

  .contentbox {
    position: absolute;
    bottom: 30px;
    left: 30px;
    color: #fff;
    font-size: 7rem;
    line-height: normal;
    opacity: 0;
    animation-fill-mode: forwards;
  }

  .contentbox p {
    margin: 0;
    line-height: 6.7rem;
  }

  .afterText {
    font-size: 2rem;
    opacity: 0;
    animation-fill-mode: forwards;
    line-height: 3rem !important;
    padding-top: 20px;
  }

  @media screen and (max-width: 768px) {
    .mainboxPageSelected {
      height: 150px;
    }
    .contentbox {
      font-size: 3rem;
    }
    .afterText {
      font-size: 1.5rem;
    }

    .interactiveParent {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
  }
</style>