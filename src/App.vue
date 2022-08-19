<script setup>
import NavBar from "./components/NavBar.vue";
// import SimplePage from "./components/SimplePage.vue";
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

import TestComponent from "./components/TestComponent.vue";
import SimplePage from "./components/SimplePage.vue";
</script>

<template>
  <nav-bar :menu="items" />
  <simple-page />
</template>
<script>
export default {
  data() {
    return {
      items: [
        { label: "Home", link: "/" },
        { label: "Blog", link: "/blog" },
        { label: "Sobre", link: "/about" },
      ],
    };
  },
  components: { NavBar, TestComponent, SimplePage },
  methods: {},
  created() {},
};
</script>
