<template>
  <div>
    <h1>Daftar Produk</h1>
    <ProductList />
  </div>
</template>

<script>
import ProductList from '~/components/ProductList.vue';

export default {
  components: {
    ProductList
  }
};
</script>

<style scoped>
h1 {
  text-align: center;
  margin-bottom: 20px;
}
</style>
