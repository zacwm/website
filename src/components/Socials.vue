<script>
import {
  BrandDiscordIcon,
  BrandGithubIcon,
  MailIcon,
} from "vue-tabler-icons";

export default {
  components: {
    BrandDiscordIcon,
    BrandGithubIcon,
    MailIcon,
  },
  methods: {
    goToURL(url) {
      // Forward to URL
      console.dir('going to ' + url + '...')
      window.location.href = url;
    },
  },
};
</script>

<template>
  <div class="socialsbox">
    <BrandDiscordIcon stroke-width="1" @click="goToURL('#about')" />
    <BrandGithubIcon stroke-width="1" @click="goToURL('https://github.com/zacimac')" />
    <MailIcon stroke-width="1" @click="goToURL('mailto:me@zachary.lol')" />
  </div>
</template>

<style>
  .socialsbox {
    position: absolute;
    top: 30px;
    right: 30px;
    line-height: normal;
    color: #ccc;
  }

  .socialsbox svg {
    height: 3rem;
    width: 3rem;
    transition: color 0.5s ease-out;
    margin-left: 1rem;
    cursor: pointer;
  }

  .socialsbox svg:hover {
    color: #fff;
  }

  @media screen and (max-width: 768px) {
    .socialsbox {
      display: flex;
      flex-direction: row;
      justify-content: space-evenly;
      position: relative;
      width: 100%;
      right: 0;
      top: 0;
      margin-top: 20px;
    }

    .socialsbox svg {
      margin-left: 0;
    }
  }
</style>