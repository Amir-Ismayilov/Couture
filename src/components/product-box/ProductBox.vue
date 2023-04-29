<template>
  <div>
    <div class="product_wrappers_one">
      <div class="thumb">
        <router-link :to="{ path: '/data/' + data[0].id }" class="image">
          <img
              :src="data[0].image"
              :alt="data[0].title"
          />
          <img
              :src="data[0].image!=null"
              :alt="data.title"
              class="hover-image"
          />
        </router-link>

        <span class="badges">
          <span class="new" v-if="data.new">Yeni</span>
          <span class="hot" v-else-if="data.hot">горячий</span>
          <span class="" v-else></span>
        </span>

      </div>

      <div class="content">
        <h5 class="title text-capitalize">
          <router-link :to="{ path: '/product/' + data.id }">{{
              data.title
            }}
          </router-link>
        </h5>
        <span class="price">
          <span class="new" v-if="data.discount  && data.discount!=0"
          >{{ discountedPrice(data) }} TRY</span
          >
          <span class="new" v-else>{{ ((this.variation_product.price * 100) / 100).toFixed(2) }} TRY</span>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
// import {mapState} from "vuex";
import product from "../../../data/product.json";


export default {
  name: "ProductBox",
  props: ["product", "index"],

  data() {
    return {
      data: product.data,
      // Product Quanity Increment/ Decrement Data
      variation_product: {
        id: 0,
        variation_id: 0,
        variation_name: "",
        created_at: "",
        updated_at: "",
        price: 0,
        sku: "",
        image: null,
        stock: 0
      },
      quantity: 1,
      imageSrc: "",
      cartProduct: {},
      compareProduct: {},
      dismissSecs: 3,
      dismissCountDown: 0,
      activeColor: "",
      selectedSize: "",
      qty: "",
      size: [],
      swiperOption: {
        slidesPerView: 1,
        spaceBetween: 20,
        freeMode: true,
      },
    };
  },
  computed: {
    swiper() {
      return this.$refs.mySwiper.swiper;
    },
  },
  mounted() {
    // console.log(this.variation_product)
    // console.log(this.product)
  },
  methods: {
    // Image Url
    // getImageUrl(path) {
    //   return require("@/assets/img/product-image/" + path);
    // },

    // Discount Price
    discountedPrice(product) {
      const price = ((this.variation_product.price * 100) / 100).toFixed(2) - (((this.variation_product.price * 100) / 100).toFixed(2) * product.discount) / 100;
      return price;
    },

    slideTo(id) {
      this.swiper.slideTo(id, 1000, false);
    },

  },
};
</script>

<style scoped>
.product_wrappers_one {
  margin-top: 30px;
}

.product_wrappers_one .thumb {
  position: relative;
  overflow: hidden;
}

.product_wrappers_one .thumb .image {
  position: relative;
  display: block;
  overflow: hidden;
}

.product_wrappers_one .thumb .image img {
  z-index: 1;
  max-width: 100%;
  transition: all 0.3s ease 0s;
  width: 100%;
  max-height: 300px;
  min-height: 300px;
}

.product_wrappers_one .thumb .image img.hover-image {
  position: absolute;
  z-index: 2;
  top: 0;
  left: 0;
  opacity: 0;
}

.product_wrappers_one .thumb .image img {
  z-index: 1;
  max-width: 100%;
  transition: all 0.3s ease 0s;
  width: 100%;
  max-height: 300px;
  min-height: 300px;
}

.product_wrappers_one .thumb .badges {
  position: absolute;
  z-index: 8;
  top: 18px;
  left: 18px;
  display: flex;
  flex-direction: column;
}

.product_wrappers_one .content {
  position: relative;
  z-index: 10;
  display: flex;
  flex-direction: column;
  padding: 20px 15px 0;
  transition: all 0.3s ease 0s;
  text-align: center;
  background-color: #f7f7f7;
}

.product_wrappers_one .content {
  position: relative;
  z-index: 10;
  display: flex;
  flex-direction: column;
  padding: 20px 15px 0;
  transition: all 0.3s ease 0s;
  text-align: center;
  background-color: #f7f7f7;
}

.product_wrappers_one .thumb .add-to-cart {
  display: block;
  width: 80%;
  height: 45px;
  line-height: 45px;
  background-color: #f7f7f7;
  text-align: center;
  border: 0;
  border-radius: 3px;
  font-size: 14px;
  position: absolute;
  bottom: 20px;
  left: 0;
  right: 0;
  z-index: 11;
  margin: auto;
  font-weight: 600;
  visibility: hidden;
  transition: all 0.3s ease 0s;
  transform: translateY(20px);
  color: #3f3f3f;
  opacity: 0;
  font-family: 'Montserrat', sans-serif;
}

.product_wrappers_one .content .title {
  font-size: 14px;
  margin: 0px 0 10px;
}

.product_wrappers_one .content .title a {
  text-decoration: none;
  color: #1d1d1d;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  display: block;
  font-size: 16px;
}

.product_wrappers_one .content .price {
  font-size: 16px;
  line-height: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #212121;
}

.product_wrappers_one .content .price span.new {
  color: #3f3f3f;
  font-weight: 500;
}
</style>