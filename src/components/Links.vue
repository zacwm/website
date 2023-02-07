<script>
import {
  ArrowBackUpIcon,
} from "vue-tabler-icons";

export default {
  props: ['page'],
  components: {
    ArrowBackUpIcon,
  },
  methods: {
    onClickLink(page) {
      this.$emit('clicked', page)
    }
  }
}
</script>

<template>
  <div class="linksbox">
    <p
      @click="onClickLink('home')"
      v-bind:style="{
        'font-weight': page === 'home' ? 400 : 200,
      }"
      v-if="page !== 'home'"
    >
      <ArrowBackUpIcon class="backIcon" stroke-width="1" />
    </p>
    <p
      @click="onClickLink('work')"
      v-bind:style="{
        'font-weight': page === 'work' ? 400 : 200,
      }"
    >
      Work
    </p>
    <p
      @click="onClickLink('about')"
      v-bind:style="{
        'font-weight': page === 'about' ? 400 : 200,
      }"
    >
      About
    </p>
  </div>
</template>

<style>
  .linksbox {
    position: absolute;
    top: 30px;
    left: 30px;
    color: #ccc;
    font-size: 2rem;
    line-height: normal;
    display: flex;
    flex-direction: row;
    z-index: 30;
    vertical-align: center;
    justify-content: center;
  }

  .linksbox .backIcon {
    height: 1.75rem;
    width: 1.75rem;
  }

  .linksbox p {
    margin: 0 20px 0 0;
    color: #ccc;
    transition: color 0.3s ease-out;
    cursor: pointer;
    user-select: none;
  }

  .linksbox p:hover {
    color: #fff;
  }

  @media screen and (max-width: 768px) {
    .linksbox {
      display: flex;
      flex-direction: row;
      justify-content: space-evenly;
      position: relative;
      width: 100%;
      top: 0;
      left: 0;
      margin-top: 20px;
    }

    .linksbox p {
      margin: 0;
    }
  }
</style>