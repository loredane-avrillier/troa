<template>
  <div>
    <app-header></app-header>
    <div class="container beers">
      <ul v-if="beers">
        <li v-for="beer of beers" :key="beer.id">
          <n-link :to="`/beers/${beer.id}`">{{ beer.name }}</n-link>
          <p>{{ beer.tagline }}</p>
          <p>{{ beer.first_brewed }}</p>

          <img :src="beer.image_url" :alt="beer.name" />
        </li>
      </ul>

      <!-- Découper en 2 composants list + modal au click bouteille passe id et infos au modal component -->
    </div>
  </div>
</template>

<script>
import AppHeader from '../components/AppHeader.vue'
export default {
  components: {
    AppHeader
  },
  async asyncData({ $axios, params, query, error }) {
    let beers = await $axios.$get("https://api.punkapi.com/v2/beers");
    return { beers };
  },
  methods: {},
};
</script>

<style>
.beers {
  position: relative;
  height: 1131px;
  width: 4776px;
}
.beers::after {
  content: "BEERS";
  position: absolute;
  transform: rotate(90deg);
  -webkit-transform: rotate(90deg);
  color: #ffcf00;
  font-family: "Druk Wide";
  font-size: 20em;
  top: 0;
  left: 0;
  z-index: -1;
  letter-spacing: 0;
  line-height: 1157px;
}
</style>
