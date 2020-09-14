<template>
  <div>
    <div class="container">
      <div class="beers">
        <!-- Beers list -->
        <ul v-if="beers">
          <li v-for="beer of beers" :key="beer.id">
            <div class="beer-details">
              <h2>{{ beer.name }}</h2>
              <p>{{ beer.tagline }}</p>
              <p>{{ beer.first_brewed }}</p>
              <div>
                <n-link class="see-more-link" :to="`/beers/${beer.id}`">SEE MORE</n-link>
              </div>
            </div>
            <!-- Pagination à la fin du BEERS jaune en bg ? -->
            <img :src="beer.image_url" :alt="beer.name" />
          </li>
        </ul>
        <!-- End beers list -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  /* function transition on index page */
  transition(to, from) {
    if (!from) {
      return "slide-left";
    }
    if (from.path == "/") {
      return "slide-left";
    }
    return "";
  },
  /* API call via Axios 
     return object beers
  */
  async asyncData({ $axios, params, query, error }) {
    let beers = await $axios.$get("https://api.punkapi.com/v2/beers");
    return { beers };
  },
};
</script>

<style lang="scss">
/* SCSS */
.beers {
  /* position relative helps to fix bg yellow text */
  position: relative;
  overflow: hidden;

  img {
    max-height: 700px;
    max-width: 180px;
  }
  /* General settings on the beer list */
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
      .see-more-link {
        border: 0;
        background-color: #000000;
        color: #ffffff;
        font-weight: bold;
        padding: 0.75em 2em;
        &:hover {
          text-decoration: none;
        }
      }
    }
  }
  /* Get reversed style for the asymetrical aspect */
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
/* Bg yellow text */
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
/* Quick responsive set up for the index page */
/* Je ne savais pas s'il fallait le faire j'ai tapé quelques lignes histoire que ça fasse propre*/
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
/* Transition page styles */
.slide-left-enter-active,
.slide-left-leave-active {
  transition: 0.3s;
}
.slide-left-enter {
  transform: translate(100%, 0);
}
.slide-left-leave-to {
  transform: translate(-100%, 0);
}
</style>
