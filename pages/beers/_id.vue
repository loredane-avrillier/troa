<template>
  <div id="beer_details">
    <!-- Layout is divided in 2 : left + right -->
    <!-- Left side -->
    <div class="side_page left_side">
      <!-- Beer name bg + img-->
      <div class="bg_name">{{ beer.name }}</div>
      <img :src="beer.image_url" :alt="beer.name" />
    </div>
    <!-- Right Side -->
    <div class="side_page right_side">
      <!-- HomePage Link + icon-->
      <n-link class="close_page" to="/">
        <icon-base width="39" height="38" viewBox="0 0 512.001 512.001" icon-name="close">
          <icon-close />
        </icon-base>
      </n-link>
      <!-- end link -->
      <!-- List of beer details -->
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
        <div class="specifications ingredients">
          <div
            class="ingredients_name_group"
            v-for="(value, name) in beer.ingredients"
            :key="'ingredients-' + name"
          >
            <span class="ingredients-name">
              <b>{{ name }}</b>
            </span>
            <div class="ingredients_details">
              <template v-if="Array.isArray(value)">
                <span
                  v-for="(ingredient, ingredient_index) in value"
                  :key="'ingredient-'  + ingredient_index"
                >{{ingredient.name}}</span>
              </template>
              <template v-else>{{value}}</template>
            </div>
          </div>
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
      <!-- end list details -->
    </div>
    <!-- end right side -->
  </div>
</template>
<script>
/* icons */
import IconBase from "../../components/IconBase.vue";
import IconClose from "../../components/icons/IconClose.vue";

export default {
  components: {
    IconBase,
    IconClose,
  },
  /* API call via Axios
    return object beer 
  */
  async asyncData({ $axios, params }) {
    let response = await $axios.get(
      `https://api.punkapi.com/v2/beers/${params.id}`
    );
    let newResponse = response.data[0];

    return { beer: newResponse };
  },
};
</script>
<style lang="scss">
#beer_details {
  /* default styles */
  display: flex;
  .side_page {
    flex-basis: 50%;
    position: relative;
    overflow: hidden;
    padding: 4em 0;
  }
  /* Left side of the page */
  .left_side {
    text-align: center;
  }
  .bg_name {
    font-size: 80px;
    position: absolute;
    z-index: -1;
    left: 0;
    top: 20%;
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
  /* Right Side of the page */
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
    .food_pairing,
    .ingredients {
      flex-direction: column;
    }
    .food_pairing span {
      margin: 0.5em 0;
    }
  }
  .ingredients-name {
    text-transform: uppercase;
  }
  .ingredients_name_group {
    display: flex;
    justify-content: space-between;
    margin: 0.5em 0;
  }
  .ingredients_details {
    display: flex;
    flex-direction: column;
    text-align: right;
    font-family: "Helvetica Neue";
    font-size: 14px;
    letter-spacing: 0;
    line-height: 22px;
  }
  /* Icon close */
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
/* media queries ipad mobile version */
@media (max-width: 768px) {
  #beer_details {
    flex-flow: column-reverse;
     .right_side {
      padding-left: 1em;
      padding-right: 1em;
    }
    .close_page {
      top: 8px;
    }
  }
 }

</style>