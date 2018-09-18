<template>
  <div class="filters">
    <h4 class="filter-header">Categories</h4>
    <ul class="categories-list">
      <li>All products</li>
      <li>New</li>
      <li>On Sale</li>
      <li>Mens</li>
      <li>Womens</li>
      <li>Shirts</li>
      <li>Bags</li>
    </ul>
  </div>
</template>


<script>
export default {
  data(){
    return {
      filter: 'products'
    }
  },
  methods: {
    update(){
      this.$emit('filterChange', this.filter);
    }
  }
}
</script>

<style>
.filters{
  display: flex;
  flex-direction: column;
  justify-content: center;
  background: white;
}
.filter-header{
  font-size: 15px;
  text-transform: capitalize;
  padding-left: 20px;
  font-weight: bold;
  opacity: 0.7;
}

.categories-list{
  list-style: none;
  padding-left: 0;
  padding-left: 40px;
  border-top: 1px solid rgba(0,0,0,0.1);
  padding-top: 15px;
  margin-top: 10px;
}

.categories-list > li{
  font-size: 14px;
  margin: 12px 0;
  color: rgba(0,0,0,0.4);
  cursor: pointer;
}

.categories-list > li:hover{
  color: rgb(73, 73, 245);
}
</style>
