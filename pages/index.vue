<template>
  <div>
    <div class="container">
      <div class="beers">
        <ul v-if="beers">
          <li v-for="beer of beers" :key="beer.id">
            <div class="beer-details">
              <h2>{{ beer.name }}</h2>
              <p>{{ beer.tagline }}</p>
              <p>{{ beer.first_brewed }}</p>
              <div>
                <!-- <button class="btn-see-more" type="button">SEE MORE</button> -->
                <n-link :to="`/beers/${beer.id}`">SEE MORE</n-link>

                <!--   <b-button v-b-toggle.sidebar-right>Toggle Sidebar</b-button> -->
                <!--      <b-sidebar id="sidebar-right" title="Sidebar" right shadow>
                  <div class="px-3 py-2">
                    <p>
                      Cras mattis consectetur purus sit amet fermentum. Cras justo odio, dapibus ac facilisis
                      in, egestas eget quam. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.
                    </p>
                    <b-img src="https://picsum.photos/500/500/?image=54" fluid thumbnail></b-img>
                  </div>
                </b-sidebar>-->
              </div>
            </div>
            <!-- Pagination à la fin du BEERS jaune en bg ? -->

            <img :src="beer.image_url" :alt="beer.name" />
          </li>
        </ul>
      </div>

      <!-- Découper en 2 composants list + modal au click bouteille passe id et infos au modal component -->
    </div>
  </div>
</template>

<script>
export default {
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
  overflow: hidden;

  img {
    max-height: 700px;
    max-width: 180px;
  }
  ul {
    list-style: none;
    padding: 0;
  }
  ul li:not(:first-child) {
    margin-top: -20%;
  }
  ul li {
    display: flex;
    padding-top: 2em;
    padding-bottom: 2em;

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
  top: -5%;
  right: 0;
  left: 0;
  z-index: -1;
  letter-spacing: 0;
  max-width: 100%;
}
@media (max-width: 768px) {
  .beers::after {
    display: none;
  }
  .beers {
    ul li {
      margin-top: 0;
    }
    ul li:nth-child(even),
    ul li:nth-child(odd) {
      flex-flow: column-reverse;
      justify-content: center;
      background-color: #ffcf00;
      margin-bottom: 5em;
      .beer-details {
        text-align: center;
        padding: 2em 0;
      }
      img {
        align-self: center;
      }
    }
  }
}
/*  line-height: 1157px;
  height: 1131px; */
/*   .b-sidebar-outer {
    z-index: 1;
  }
  .b-sidebar {
    top: 9em;
    width: 100%;
  } */
</style>
