<template>
  <section id="product-page">
    <template v-if="meal">
        <ProductCom :meal="meal" />
    </template>
    <template v-else>
        Loading...
    </template>
  </section>
</template>

<script>
import axios from "axios";
import ProductCom from '@/components/ProductPage/ProductCom.vue';
export default {
  components: { ProductCom },
  name: "ProductView",
  data() {
    return {
      meal: {},
    };
  },
  mounted() {
    const id = this.$route.params.id;
    axios
      .get(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${id}`)
      .then((res) => {
        this.meal = res.data.meals[0];
      }).catch(err => {
        console.log(err.message)
      })
  },
};
</script>

<style scoped>
#product-page {
    width: 100vw;
    width: 100dvw;
    height: calc(100vh - 144px);
    height: calc(100dvh - 144px);
    padding: 20px;
    overflow-y: scroll;
    background-color: var(--color3);
}
</style>