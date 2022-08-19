<template>
  <nav
    class="navbar"
    :class="theme"
    role="navigation"
    aria-label="main navigation"
  >
    <div class="navbar-brand">
      <a class="navbar-item" href="https://bulma.io"> </a>

      <a
        role="button"
        class="navbar-burger"
        aria-label="menu"
        aria-expanded="false"
        data-target="navbarBasicExample"
      >
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>

    <div id="navbarBasicExample" class="navbar-menu">
      <div class="navbar-start">
        <a class="navbar-item" :href="item.link" :key="item" v-for="item in menu">{{ item.label }}</a>

        <!-- <a class="navbar-item"> Documentation </a> -->
      </div>

      <div class="navbar-end">
        <div class="navbar-item">
          <div class="buttons">
            <button class="button" @click="changeTheme()">
              <i
                class="fas"
                :class="this.theme == 'is-dark' ? 'fa-sun' : 'fa-moon'"
              ></i>
            </button>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      theme: "",
    };
  },
  props:{
    menu:Array
  },
  methods: {
    getTheme() {
      let theme = sessionStorage.getItem("theme");
      this.theme = theme ? theme : "is-light";
      this.changeStyle();
      sessionStorage.setItem("theme", this.theme);
    },
    changeTheme() {
      let theme = this.theme == "is-light" ? "is-dark" : "is-light";
      this.theme = theme;
      this.changeStyle();
      sessionStorage.setItem("theme", this.theme);
    },
    changeStyle() {
      let body = document.querySelector("html");
      body.setAttribute("class", this.theme);
    },
  },
  created() {
    this.getTheme();
  },
};
</script>

<style>
html.is-dark, section.is-dark {
  background-color: dimgray !important;
}
html.is-light {
  background-color: rgb(236, 230, 223)!important;
}


</style>
