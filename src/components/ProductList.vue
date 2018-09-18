<template>
  <div class="product-list">
    <product v-for="product of products" :key="product.id" :product="product" />
  </div>
</template>

<script>
import Product from './Product';

export default {
  name: 'ProductList',
  props: {
    products: Array
  },
  components: {
    Product
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .product-list{
    display: flex;
    flex-wrap: wrap;
  }
</style>
