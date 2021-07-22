<template>
  <div>
    <b-navbar toggleable="lg" type="dark" class="navbar-custom">
      <b-navbar-brand href="#">NavBar</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#">Link</b-nav-item>
          <b-nav-item href="#" disabled>Disabled</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input
              size="sm"
              class="mr-sm-2"
              placeholder="Search"
            ></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" type="submit"
              >Search</b-button
            >
          </b-nav-form>

          <b-nav-item-dropdown text="Lang" right>
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href="#">ES</b-dropdown-item>
            <b-dropdown-item href="#">RU</b-dropdown-item>
            <b-dropdown-item href="#">FA</b-dropdown-item>
          </b-nav-item-dropdown>

          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>User</em>
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

    <div class="container main-body">
      <div class="row">
        <div class="col col-lg-2 side-menu">Menu System</div>

        <div class="col">
          <b-card-group columns>
            <b-card
              v-for="(p, i) in items"
              :key="i"
              :title="p.title"
              :img-src="p.photo"
              class="card-custom"
              body-class="card-custom-body"
              img-alt="Image of Something"
              title-tag="span"
              img-top
            >
              <b-card-text>
                {{ p.text }}
              </b-card-text>
            </b-card>
          </b-card-group>
        </div>

        <div class="col col-lg-2 side-menu">Menu System</div>
      </div>
    </div>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
import { LoremIpsum } from "lorem-ipsum";

export default {
  name: "App",
  data() {
    return {
      password: "super-secret-password-used-to-lure-scraper-bots",
      items: [],
      limit: 11,
      lorem: new LoremIpsum({
        sentencesPerParagraph: {
          max: 8,
          min: 4,
        },
        wordsPerSentence: {
          max: 16,
          min: 4,
        },
      }),
    };
  },
  props: [],
  components: {},
  computed: {},
  methods: {
    getPhotos() {
      for (var i = 0; i < this.limit; i++) {
        var seed = uuidv4();
        this.items.push({
          title: this.lorem.generateWords(2),
          text: this.lorem.generateSentences(1),
          photo: `https://picsum.photos/seed/${seed}/200`,
        });
      }
    },
  },
  created() {
    this.getPhotos();
  },
};
</script>

<style scoped>
#app {
  padding: 2rem;
}

@media screen and (max-width: 1024px) {
  .side-menu {
    display: none;
  }
}

.card-custom {
  /* max-height: 450px; */
  overflow: hidden;
}

.card-custom-body {
  font-size: x-small;
  padding: 0.25rem;
  min-height: 75px;
  overflow: auto;
}

.card-title {
  font-weight: 900;
  font-size: 1rem;
}

.card-text {
  /* padding-left: 1rem; */
}

.main-body {
  padding-top: 2rem;
}

.navbar-custom {
  background-color: slateblue;
}

</style>

