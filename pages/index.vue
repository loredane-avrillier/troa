<template>
  <!-- <div class="container">
    <div>
      <Logo />
      <h1 class="title">
        troa
      </h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>-->
  <div>
    <h1>Troa test</h1>
<!--     <div>
          {{ beers }}
    </div> -->

    <ul v-if="beers">
      <li v-for="beer of beers" :key="beer.id">
        <n-link :to="`/beers/${beer.id}`">{{ beer.name }}</n-link>
        <p>{{ beer.tagline }}</p>
        <p>{{ beer.first_brewed }}</p>

         <img :src="beer.image_url" :alt="beer.name">
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios, params, query, error }) {
    let beers = await $axios.$get("https://api.punkapi.com/v2/beers");
    return { beers };
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
