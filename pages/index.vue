<template>
  <div>
    <app-header></app-header>
    <div class="container">
      <div class="beers">
        <ul v-if="beers">
          <li v-for="beer of beers" :key="beer.id">
            <div class="beer-details">
              <h2>{{ beer.name }}</h2>
              <p>{{ beer.tagline }}</p>
              <p>{{ beer.first_brewed }}</p>
              <div>
                <button class="btn-see-more" type="button">SEE MORE</button>
              </div>
            </div>

            <img :src="beer.image_url" :alt="beer.name" />
          </li>
        </ul>
      </div>

      <!-- Découper en 2 composants list + modal au click bouteille passe id et infos au modal component -->
    </div>
  </div>
</template>

<script>
import AppHeader from "../components/AppHeader.vue";
export default {
  components: {
    AppHeader,
  },
  async asyncData({ $axios, params, query, error }) {
    let beers = await $axios.$get("https://api.punkapi.com/v2/beers");
    return { beers };
  },
  methods: {},
};
</script>

<style lang="scss">
.beers {
  position: relative;

  img {
    max-height: 700px;
    max-width: 180px;
  }
  ul {
    list-style: none;
  }
  ul li {
    display: flex;
    margin: 2em auto;
    .beer-details {
      display: flex;
      flex-direction: column;
      flex-basis: 30%;
      align-self: center;

      p {
        font-family: "Helvetica Neue";
        font-size: 20px;
        font-weight: bold;
        letter-spacing: 0;
      }
      h2 {
        color: #000000;
        font-size: 80px;
        letter-spacing: 0;
        line-height: 64px;
        font-family: "Druk-Cond-Super";
      }
      .btn-see-more {
        border: 0;
        background-color: #000000;
        color: #ffffff;
        font-weight: bold;
        padding: 0.75em 2em;
      }
    }
  }
  ul li:nth-child(even) {
    .beer-details {
      padding-left: 3em;
    }

    flex-flow: row-reverse;
  }
  ul li:nth-child(odd) {
    .beer-details {
      text-align: right;
      padding-right: 3em;
    }
  }
}
.beers::after {
  content: "BEERS";
  position: absolute;
  transform: rotate(90deg);
  -webkit-transform: rotate(90deg);
  color: #ffcf00;
  font-family: "Druk-Wide-Super";
  font-size: 884px;
  top: 0;
  right: 0;
  left: 0;
  z-index: -1;
  letter-spacing: 0;
  line-height: 1157px;
  height: 1131px;
}
</style>
