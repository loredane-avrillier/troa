<template>
  <div>
    <p>{{ beer.name }}</p>
    <p>{{ beer.description }}</p>
    <p>{{ beer.abv }}</p>INGREDIENTS
    <p
      v-for="(ingredient_detail, index) in beer.ingredients"
      :key="'ingredient_detail' + index"
    >{{index}} {{ ingredient_detail }}</p>FOOD PAIRING
    <p
      v-for="(food_pairing_detail, index) in beer.food_pairing"
      :key="'food_paring_detail' + index"
    >{{ food_pairing_detail }}</p>
  </div>
</template>
<script>
export default {
  async asyncData({ $axios, params }) {
    let response = await $axios.get(
      `https://api.punkapi.com/v2/beers/${params.id}`
    );
    console.log(response.data);
    return { beer: response.data[0] };
  },
};
</script>