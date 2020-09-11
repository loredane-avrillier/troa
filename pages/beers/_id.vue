<template>
  <div>
    details {{ beer }}
    close
  </div>
</template>
<script>
export default {
  /*   data() {
        return {
            name: ""
        }
    }, */
  asyncData({ $axios, params, error }) {
    return $axios
      .get(`https://api.punkapi.com/v2/beers/${params.id}`)
      .then((res) => {
        
        return { beer:res.data }
      })
      .catch((e) => {
        error({ statusCode: 404, message: "Produit non trouvé" });
      });
  },
};
/* asyncData({ $axios, params, error }) {
    return $axios
      .get(`https://api.punkapi.com/v2/beers/${params.id}`)
      .then(res => {
        let data = {
          id: res.data.data.id,
          slug: res.data.data.slug,
          desc: res.data.data.desc,
          main_photo: res.data.data.main_photo,
          weezea_ref: res.data.data.weezea_ref,
          colors: res.data.data.colors,
          long_desc: res.data.data.long_desc,
          dimensions: res.data.data.dimensions,
          material: res.data.data.material,
          category: res.data.data.category,
          status_id: res.data.data.status_id,
          related: [],
          sizes: res.data.data.sizes,
          seo: res.data.data.seo
        };
       return data;
      })
      .catch(e => {
        error({ statusCode: 404, message: "Produit non trouvé" });
      }); */
</script>