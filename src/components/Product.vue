<template>
  <div class="product">
    <div class="product-card">
      <div class="image-preview">
        <div class="preview">
          <a :href="product.url" target="_blank">
            <img id="productImg" class="img-responsive" :src="previewImg"  :alt="product.description || ''"/>
          </a>
        </div>
        <div class="img-thumbnails">
          <img v-for="thumb of product.thumbnails" :key="thumb" :src="getProductThumbnail(thumb)" @click="setImagePreview(thumb)" style="margin-right:4px" />
        </div>
      </div>
      <div class="details">
        <div class="extras">
          <div class="product-info">
            <h5 class="product-name">{{product.title}}</h5>
            <p class="description">{{product.description}}</p>
            <p class="discount" v-if="product.previousPrice">up to {{getPercentageDiscount(product)}}% off</p>
          </div>
          <div class="deals">
            <div class="price-offer">
              <p class="prev" v-if="product.previousPrice">{{product.previousPrice}}</p>
              <p class="current">{{product.discountPrice}}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: {},
  },
  data(){
    return {
      previewImg: ''
    }
  },
  methods: {
    getImageUrl({badge = '', image}){
      const imageWithNewBadge = 'https://res.cloudinary.com/sealuse-creatives/image/upload/q_auto,f_auto,fl_lossy,c_scale,h_370/l_new_1,w_60,g_north_west,y_60/';
      const imageWithSaleBadge = 'https://res.cloudinary.com/sealuse-creatives/image/upload/q_auto,f_auto,fl_lossy,c_scale,w_370/l_sale,w_60,g_west/';
      const defaultUrl = 'https://res.cloudinary.com/sealuse-creatives/image/upload/q_auto,f_auto,fl_lossy,c_scale,w_370/';

      const imageUrl = badge ? badge ==='new' ? `${imageWithNewBadge}${image}` : `${imageWithSaleBadge}${image}` : `${defaultUrl}${image}`
      
      return imageUrl;
    },

    getProductThumbnail(imageId){
      return `https://res.cloudinary.com/sealuse-creatives/image/upload/q_auto,f_auto,fl_lossy,w_80,h_80,c_fill/${imageId}`;
    },

    getPercentageDiscount({previousPrice, discountPrice}){
      const difference = previousPrice.slice(1) - discountPrice.slice(1);
      const percentage = difference/previousPrice.slice(1) * 100;
      return Math.round(percentage);
    },

    setImagePreview(imageId){
      // const imageTransformations = {
      //   '1': 'https://res.cloudinary.com/sealuse-creatives/image/upload/q_auto,f_auto,fl_lossy,c_fill/',
      //   '2': 'https://res.cloudinary.com/sealuse-creatives/image/upload/e_cartoonify,q_auto,f_auto,fl_lossy,c_fill/',
      //   '3': 'https://res.cloudinary.com/sealuse-creatives/image/upload/e_hue:80,q_auto,f_auto,fl_lossy,c_fill,g_auto/'
      // };

      // const preview = `${imageTransformations[position]}${this.product.image}`;

      this.previewImg = this.getImageUrl({image: imageId});
    },
    setproductImage(){
      this.previewImg = this.getImageUrl(this.product);
    }
  },
  created(){
    this.setproductImage();
  }
}
</script>


<style>
.product {
  width: 22%;
  background: white;
  border-radius: 5px;
  padding: 0;
  margin: 0 20px 30px 0;
  transition: 0.2s ease-in-out;
}

.product:hover {
  box-shadow: 0 15px 30px 0 rgba(0, 0, 0, 0.11),
    0 5px 15px 0 rgba(0, 0, 0, 0.08);
  transform: scale(1.03);
}

.img-thumbnails {
  display: flex;
  margin-top: 6px;
}

.img-thumbnails > img {
  height: 0px;
  width: 30px;
  object-fit: cover;
  border-radius: 4px;
  margin: 0 3px;
  transition: 0.4s ease-in-out;
  cursor: pointer;
}

.product:hover .img-thumbnails > img {
  height: 30px;
}

.image-preview {
  display: flex;
  flex-direction: column;
  padding: 0;
}

.preview {
  width: 100%;
}

.preview img {
  max-height: 200px;
  max-width: 100%;
  width: 100%;
  object-fit: cover;
}

.product-info {
  max-width: 80%;
}

.product-info .product-name {
  font-size: 12px;
  text-transform: uppercase;
  font-weight: 500;
  opacity: 0.6;
  margin: 5px 0;
}

.product-info .description {
  font-size: 11px;
  opacity: 0.5;
  font-weight: 500;
  margin: 2px 0;
}

.extras {
  display: flex;
  justify-content: space-between;
  padding: 10px 15px;
}

.product-info > .discount {
  font-size: 12px;
  color: rgb(219, 55, 55);
  font-weight: 500;
  margin-top: 8px;
}

.price-offer {
  width: fit-content;
  padding: 5px;
  background: rgba(0, 0, 0, 0.03);
  box-shadow: 1px 1px 1px 0 rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.deals .prev {
  font-size: 12px;
  opacity: 0.5;
  font-weight: 500;
  margin: 5px 0;
  position: relative;
}

.deals .current {
  font-size: 14px;
  opacity: 0.8;
  font-weight: bold;
  margin: 0;
}

.deals .prev:after {
  content: '';
  position: absolute;
  width: 60%;
  height: 2px;
  background: red;
  left: 0;
  top: 40%;
}

.colors {
  display: flex;
  padding: 10px 15px;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
}

.color {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  margin: 0 3px;
}

.color.selected {
  border: 1px solid rgba(0, 0, 0, 0.6);
}

.color.red {
  background: rgb(214, 29, 29);
}
.color.green {
  background: rgb(23, 207, 23);
}
.color.blue {
  background: rgb(70, 70, 230);
}
.color.orange {
  background: orange;
}
</style>
