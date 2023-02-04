<script lang="ts">
import Links from './Links.vue';
import Socials from './Socials.vue';

export default {
    data() {
        return {
            mouseX: 0,
            mouseY: 0
        };
    },
    created() {
        document.addEventListener("mousemove", this.updateMousePosition);
        this.$nextTick(function () {
            const contentbox = document.querySelector(".mainbox");
            if (contentbox) {
                contentbox.classList.add("fadeInUp");
            }
            else {
                console.error("mainbox not found");
            }
            setTimeout(() => {
                const contentbox = document.querySelector(".contentbox");
                if (contentbox) {
                    contentbox.classList.add("fadeInUp");
                }
                else {
                    console.error("contentbox not found");
                }
            }, 1500);
            setTimeout(() => {
                const afterText = document.querySelector(".afterText");
                if (afterText) {
                    afterText.classList.add("fadeInUp");
                }
                else {
                    console.error("afterText not found");
                }
            }, 2500);
        });
    },
    beforeDestroy() {
        document.removeEventListener("mousemove", this.updateMousePosition);
    },
    computed: {
        backgroundPosition() {
            // only move background around a fixed size of the screen
            const maxMovement = 100;
            const x = this.mouseX / window.innerWidth;
            const y = this.mouseY / window.innerHeight;
            const xMovement = (x - 0.5) * maxMovement;
            const yMovement = (y - 0.5) * maxMovement;
            // subtract 50px to center the background
            return `${xMovement - 50}px ${yMovement - 50}px`;
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
        }
    },
    components: { Links }
}
</script>

<template>
  <div
    class="mainbox"
    v-bind:style="{
      'background-position': backgroundPosition,
      'background-image': 'url(' + randomBackgroundInt + ')'
    }"
  >
    <div class="blurbox">
      <Links />
      <Socials />
      <div class="contentbox">
        <p>Hi,</p>
        <p>I'm Zachary</p>
        <p class="afterText">A full stack developer from Brisbane, Australia</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .fadeInUp {
    animation: fadeInUp 1s ease-in-out;
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
  .mainbox {
    position: relative;
    height: 100%;
    width: 100%;
    background-color: #333;
    border-radius: 40px;
    background-size: 110%;
    transition: background-position 0.5s ease-out;
    background-repeat: no-repeat;
    background-position: center;
    overflow: hidden;
    box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.5);
    opacity: 0;
    animation-fill-mode: forwards;
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

  .afterText {
    font-size: 2rem;
    opacity: 0;
    animation-fill-mode: forwards;
  }

  .contentbox p {
    margin: 0;
  }
</style>