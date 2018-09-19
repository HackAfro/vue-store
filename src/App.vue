<template>
  <div id="app">
    <div class="hero">
      <div class="container">
        <div class="heading">
          <h4>There's always beauty around you</h4>
          <p>Visit our online store to experience the beauty in our collection</p>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="filter-area">
        <product-filter @filterChange="updateProductList" />
      </div>
      <div class="product-area">
        <product-list :products="products" />
      </div>
    </div>
  </div>
</template>

<script>
import ProductFilter from './components/ProductFilter'
import ProductList from './components/ProductList';

export default {
  name: 'app',
  components: {
    ProductFilter,
    ProductList
  },
  data(){
    return {
      filter: 'products',
      products: [],
    }
  },
  methods: {
    async updateProductList(query){
      this.filter = query;
      const resourceUrl = this.getResourceUrl(this.filter);
      const res = await fetch(resourceUrl);
      const resJson = await res.json();
      this.products = resJson;
    },
    getResourceUrl(filter = ''){
      return `http://localhost:4000/products/${filter}`;
    }
  },
  created(){
    this.updateProductList();
  }

}
</script>

<style>
body {
  font-family: 'Roboto';
  background: rgba(0, 0, 0, 0.03);
}
.navbar {
  margin-bottom: 0;
  border-radius: 0;
  background-color: white;
  border-color: white;
  box-shadow: 0 2px 1px 0 rgba(0, 0, 0, 0.1);
}

.navbar .container {
  display: flex;
  align-items: center;
}

#app {
  color: #2c3e50;
}

input {
  outline: none !important;
}

footer div.container {
  float: right;
  text-align: right;
  margin-top: 100px;
  color: #ccc;
}
#app div.container {
  margin: 0 auto;
}
.flushtop {
  font-size: 18px;
  font-weight: bold;
  color: rgba(0, 0, 0, 0.7);
  text-transform: capitalize;
  line-height: 1.6;
  font-family: 'Pacifico', cursive;
}
#qualityForm {
  margin-bottom: 50px;
}

.hero {
  height: 400px;
  width: 100%;
  background: linear-gradient(0deg, #4a4646, #4a4646),
    url(https://images.unsplash.com/photo-1512436991641-6745cdb1723f?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=ad25f4eb5444edddb0c5fb252a7f1dce&auto=format&fit=crop&w=1500&q=80)
      no-repeat;
  background-blend-mode: multiply, normal;
  background-size: cover;
}

.hero .container{
  height: 100%;
}

.hero .heading{
  display: flex;
  height: 100%;
  justify-content: center;
  flex-direction: column;
}

.heading h4{
  font-size: 45px;
  font-weight: 700;
  color: white;
  font-family: 'Pacifico', cursive;
}

.heading p{
  font-size: 20px;
  font-weight: 400;
  opacity: 0.7;
  color: white;
}

.content{
  display: flex;
  margin-top: 35px;
}

.filter-area{
  width: 15%;
}

.product-area{
  width: 80%;
  margin-left: 1%;
}

a,
a:hover,
a:visited,
a:active,
a:link {
  text-decoration: none;
  color: black;
}
</style>
