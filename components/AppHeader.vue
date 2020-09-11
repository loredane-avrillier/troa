<template>
  <div>
    <b-navbar variant="faded" type="light">
      <b-navbar-brand tag="h1" class="mb-0">
        <n-link to="/">B</n-link>
      </b-navbar-brand>
      <a class="apple-emoji-beer" href="#">🍺</a>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "AppHeader",
};
</script>
<style scoped lang="scss">
.navbar-expand {
  justify-content: space-between;
}
nav {
  border-bottom: 1px solid lightgray;
  .navbar-brand a {
    color: #000000;
    font-family: "Druk Cond";
    font-size: 80px;
    letter-spacing: 0;
    &:hover {
        text-decoration: none;
    }
    font-family: "Druk-Cond-Super";
  }
  .apple-emoji-beer {
    height: 66px;
    width: 50px;
    color: #000000;
    font-family: "Apple Color Emoji";
    font-size: 50px;
    letter-spacing: 0;
    line-height: 66px;
    &:hover {
        text-decoration: none;
    }
  }
}
</style>