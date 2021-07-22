<template>
  <div id="app">
    <div>
      <b-card-group columns>
        <b-card
          v-for="(p, i) in items"
          :key="i"
          :title="p.title"
          :img-src="p.photo"
          class="card-custom"
          body-class="card-custom-body"
          img-alt="Image of Something"
          img-top
        >
          <b-card-text>
            {{ p.text }}
          </b-card-text>
        </b-card>
      </b-card-group>
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
      items: [],
      limit: 25,
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

.card-custom {
  max-height: 500px;
}

.card-custom-body {
  font-size: x-small;
}
</style>

