<template>
  <div id="beer_details">
    <div class="side_page">
      
      <div class="bg_name">{{ beer.name }}</div>
      <img :src="beer.image_url" :alt="beer.name" />
    </div>
    <div class="side_page">desc</div>
    <!-- <p>{{ beer.name }}</p>
    <p>{{ beer.description }}</p>
    <p>{{ beer.abv }}</p>
    <br> INGREDIENTS <br>
    <div
      v-for="(ingredient_detail, ingredient_detail_index) in beer.ingredients"
      :key="'ingredient_detail' + ingredient_detail_index"
    >
    {{ingredient_detail_index}} {{ ingredient_detail }}
    
    </div>
    
    
    
    <br> 
    
    FOOD PAIRING 

    <br>
    <p
      v-for="(food_pairing_detail, index) in beer.food_pairing"
      :key="'food_paring_detail' + index"
    >{{ food_pairing_detail }}</p>-->
  </div>
</template>
<script>
var flatten = require("flat");
export default {
  async asyncData({ $axios, params }) {
    let response = await $axios.get(
      `https://api.punkapi.com/v2/beers/${params.id}`
    );
    let newResponse = response.data[0];
    /*    var result = Object.entries(newResponse.ingredients);
 
   console.log(result);
   var array = Object.keys(newResponse.ingredients)
    .map(function(key) {
        return newResponse.ingredients[key];
    });

console.log(array);  */
    console.log(newResponse);
    return { beer: newResponse };
  },
};
</script>
<style lang="scss">
#beer_details {
  display: flex;
  .side_page {
    flex-basis: 50%;
    position: relative;
  }
  .bg_name {
    font-size: 80px;
    position: absolute;
    z-index: -1;
    top: 0;
    left: 0;
    bottom: 0;
  }
}
</style>