<!-- <script setup>
import HelloWorld from "./components/HelloWorld.vue";
</script> -->

<template>
  <!-- <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div> -->
  <div class="text-center">
    <HelloWorld msg="Vite + Vue" />
    <GENLINK msg="GEN LINK GOOGLE DRIVE" />
    <Sample />
  </div>
</template>

<script>
import GENLINK from "./components/GenLink.vue";
import HelloWorld from "./components/HelloWorld.vue";
import Sample from "./components/SAMPLE.vue";
export default {
  components: {
    GENLINK,
    HelloWorld,
    Sample,
  },
  data() {
    return {};
  },
  created() {},
  mounted() {},
  methods: {},
};
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
