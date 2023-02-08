<script lang="ts">
export default {
  directives: {
    tooltip: {
      inserted(el, binding) {
        el.classList.add('tooltip');
        const text = document.createElement('span');
        text.classList.add('tooltip-text');
        text.innerText = binding.value;
        el.appendChild(text);
      },
    },
  },
};
</script>

<template>
  <div class="aboutContentParent">
    <p>Hi, I'm Zachary, a 20-year-old full-stack developer from Brisbane, Australia.</p>
    <p>I'm pursuing a Bachelor of Science in Information Technology and have been teaching myself since 2015, when I received my first laptop.</p>
    <p>My experience consists of:</p>
    <table>
      <tr>
        <td>Frontend</td>
        <td>HTML, CSS, JavaScript, TypeScript, <span v-tooltip="'This website is made in Vue!'">Vue.js</span>, React.js, jQuery, Bootstrap</td>
      </tr>
      <tr>
        <td>Backend</td>
        <td>Node.js, Express.js, MySQL, MongoDB</td>
      </tr>
      <tr>
        <td></td>
      </tr>
      <tr>
        <td>Other</td>
        <td>Git, Linux, Bash, Nginx, C++, Java, Python</td>
      </tr>
    </table>
    <p>I'm available for comissions, <a href="mailto:me@zachary.lol">contact me</a></p>
  </div>
</template>

<style scoped>
* {
  color: #ccc;
  font-size: 1.5rem;
  line-height: normal;
}

.aboutContentParent {
  padding: 0 30px;
}

td {
  padding-right: 1rem;
}

td:first-child {
  font-weight: 400;
}

.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltip-text {
  visibility: hidden;
  width: 120px;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;
  position: absolute;
  z-index: 1;
  bottom: 150%;
  left: 50%;
  margin-left: -60px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip:hover .tooltip-text {
  visibility: visible;
  opacity: 1;
}
</style>