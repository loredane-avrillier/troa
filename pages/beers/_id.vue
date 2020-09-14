<template>
  <div id="beer_details">
    <div class="side_page left_side">
      <div class="bg_name">{{ beer.name }}</div>
      <img :src="beer.image_url" :alt="beer.name" />
    </div>
    <div class="side_page right_side">
      <n-link class="close_page" to="/">
        <icon-base width="39" height="38" viewBox="0 0 512.001 512.001" icon-name="close">
          <icon-close />
        </icon-base>
      </n-link>
      <h1>{{ beer.name }}</h1>
      <p class="description">{{ beer.description }}</p>
      <div>
        <h2>Spécifications</h2>
        <div class="specifications">
          <span>
            <b>ABV</b>
          </span>
          <span>{{ beer.abv }}</span>
        </div>
      </div>
      <div>
        <h2>Ingrédients</h2>
        <div class="specifications">
          <span>
            <b>MALT</b>
          </span>
        </div>
        <div class="specifications">
          <span>
            <b>YEAST</b>
          </span>
        </div>
      </div>
      <div>
        <h2>Food pairing</h2>
        <div class="specifications food_pairing">
          <span
            v-for="(food_pairing_detail, index) in beer.food_pairing"
            :key="'food_paring_detail' + index"
          >{{ food_pairing_detail }}</span>
        </div>
      </div>
    </div>
    <!-- 
    <br> INGREDIENTS <br>
    <div
      v-for="(ingredient_detail, ingredient_detail_index) in beer.ingredients"
      :key="'ingredient_detail' + ingredient_detail_index"
    >
    {{ingredient_detail_index}} {{ ingredient_detail }}
    
    </div>-->
  </div>
</template>
<script>
import IconBase from "../../components/IconBase.vue";
import IconClose from "../../components/icons/IconClose.vue";
var flatten = require("flat");
export default {
  components: {
    IconBase,
    IconClose,
  },
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
    overflow: hidden;
    padding: 4em 0;
  }
  .left_side {
    text-align: center;
  }
  .bg_name {
    font-size: 80px;
    position: absolute;
    z-index: -1;
    left: 0;
    bottom: 20%;
    color: #ffce00;
    font-family: "Druk-Cond-Super";
    font-size: 400px;
    letter-spacing: 0;
    text-transform: uppercase;
    text-align: center;
    height: 616px;
    width: 718px;
    line-height: 308px;
  }
  .right_side {
    padding-left: 8em;
    padding-right: 8em;
    position: relative;
    h1 {
      width: 420px;
      color: #000000;
      font-family: "Druk-Cond-Super";
      font-size: 80px;
      letter-spacing: 0;
      line-height: 64px;
      text-transform: uppercase;
    }
    .description {
      padding: 4em 0;
      color: #000000;
      font-family: "Helvetica Neue";
      font-size: 14px;
      letter-spacing: 0;
      line-height: 22px;
    }
    h2 {
      height: 30px;
      width: 240px;
      color: #cccccc;
      font-family: "Helvetica Neue";
      font-size: 20px;
      font-weight: bold;
      letter-spacing: 0;
      line-height: 30px;
      text-transform: uppercase;
      margin: 1.5em 0;
    }
    .specifications {
      display: flex;
      justify-content: space-between;
      border-top: 1px solid #d8d8d8;
      padding: 1em 0;
    }
    .specifications:last-child {
      border-bottom: 1px solid #d8d8d8;
    }
    .food_pairing {
      flex-direction: column;
      span {
        margin: 0.5em 0;
      }
    }
  }
  .close_page {
    position: absolute;
    top: 2%;
    left: 0;
    color: #000000;
    height: 38px;
    width: 39px;
    &:hover {
      text-decoration: none;
      color: #000000;
    }
  }
}
</style>