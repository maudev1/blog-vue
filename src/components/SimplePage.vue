<template>
  <div id="app" class="col-sm-12">
    <div class="offset">
      <section class="section posts">
        <div class="columns">
          <div class="column">
            <div
              class="card"
              :class="theme"
              :key="p"
              v-for="p in displayedPosts"
            >
              <div class="card-content">
                <h2 class="subtitle" :class="theme">{{ p.title }}</h2>
              </div>
              <div class="card-content">
                <div class="content">
                  {{ p.body }}
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
      <section class="section">
        <nav>
          <ul class="pagination">
            <li class="page-item">
              <button
                type="button"
                class="button is-small page-link"
                v-if="page != 1"
                @click="page--"
              >
                Anterior
              </button>
            </li>
            <li class="page-item">
              <!-- <button
                type="button"
                class="button is-small page-link"
                :key="pageNumber"
                v-for="pageNumber in pages.slice(page - 1, page + 5)"
                @click="page = pageNumber"
              > -->
              <button
                type="button"
                class="button is-small page-link"
                :key="pageNumber"
                v-for="pageNumber in pages"
                @click="page = pageNumber"
              >
                {{ pageNumber }}
              </button>
            </li>
            <li class="page-item">
              <button
                type="button"
                @click="page++"
                v-if="page < pages.length"
                class="button is-small page-link"
              >
                Próximo
              </button>
            </li>
          </ul>
        </nav>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
      page: 1,
      perPage: 2,
      pages: [],
      theme: "",
    };
  },
  methods: {
    async getPosts() {
      await axios.get("http://localhost/index.php").then((response) => {
        this.items = response.data;
        this.setPages();
      });
    },
    setPages() {
      let numberOfPages = Math.ceil(this.items.length / this.perPage);
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate(posts) {
      let page = this.page;
      let perPage = this.perPage;
      let from = page * perPage - perPage;
      let to = page * perPage;
      return posts.slice(from, to);
    },
    getTheme() {
      let theme = sessionStorage.getItem("theme");
      this.theme = theme ? theme : "is-light";
      sessionStorage.setItem("theme", this.theme);
     
    },
  },
  computed: {
    displayedPosts() {
      return this.paginate(this.items);
    },
  },
  watch: {
    pages() {
      this.setPages();
    },
  },
  filters: {
    trimWords(value) {
      return value.split(" ").splice(0, 20).join(" ") + "...";
    },
  },
  created() {
    this.getPosts();
    this.setPages();
    this. getTheme();
  },
};
</script>

<style>
@font-face {
  font-family: 'roboto';
  src: url('src/assets/Roboto-Regular.ttf');
}
.card {
  margin-bottom: 30px;
}

.card.is-dark{
  background-color:#363636;
  color:white;
  font-family: 'roboto';
}
.card {
  width: 100%;
  border-radius: 0;
}

.subtitle.is-dark{
  color:white !important
}

.page-link {
  margin: 5px;
}
</style>