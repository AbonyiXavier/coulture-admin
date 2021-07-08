<template>
  <main>
    <div class="a-spacing-large"></div>
    <div class="container-fluid browsing-history">
      <div class="row">
        <div class="col-sm-8 col-8">
          <h1 class="a-size-large a-spacing-none a-text-normal">
            All products
          </h1>
          <!-- Button -->
          <div class="a-spacing-large"></div>
          <nuxt-link
            to="/products"
            class="a-button-buy-again"
            style="margin-right: 10px;"
            >Add a new product</nuxt-link
          >
        </div>
      </div>
    </div>
    <div class="a-spacing-large"></div>
    <div class="container-fluid browsing-history">
      <div class="row">
        <div
          v-for="(product, index) in products"
          :key="product._id"
          class="col-xl-2 col-lg-2 col-md-2 col-6 br bb"
        >
          <div class="history-box">
            <!-- Product Image -->
            <a href="" class="a-link-normal">
              <img
                :src="`https://coulture-backend.herokuapp.com/${product.photo}`"
                alt="image"
                class="img-fluid"
              />
            </a>
            <div class="a-spacing-top-base asin-title">
              <span class="a-text-normal">
                <div class="p13-sc-truncated">
                  {{ product.title }}
                </div>
              </span>
            </div>
            <div class="a-row">
              <a href="#">
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
              </a>
              <span class="a-letter-space"></span>
            </div>
            <!-- Product Price -->
            <div class="a-row">
              <span class="a-size-base a-color-price">
                <!-- <span class="p13-sc-price">{{
                  moneyFormatter(product.price)
                }}</span> -->
                <span class="p13-sc-price">${{ product.price }}</span>
              </span>
            </div>
            <!-- Product Button -->
            <div class="a-row">
              <nuxt-link
                :to="`/products/${product._id}`"
                class="a-button-history margin-right-10"
                >Update</nuxt-link
              >
              <a
                href="#"
                class="a-button-history margin-right-10"
                @click="onDeleteProduct(product._id)"
                >Delete</a
              >
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      products: "",
    };
  },
  //asyncData is fetching data before nuxt page finished loading on the server
  // it is good for seo because the data will be loaded first
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get(
        "https://coulture-backend.herokuapp.com/api/products"
      );
      // console.log("image", response);
      return {
        products: response.products,
      };
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async onDeleteProduct(id, index) {
      try {
        let response = await this.$axios.$delete(
          `https://coulture-backend.herokuapp.com/api/products/${id}`
        );
        if (response.status) {
          // remove
          this.products.splice(index, 1);
        }
      } catch (err) {
        console.log(err);
      }
    },

    moneyFormatter(num) {
      const profits = num.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, "$&,");
      return `${"#"}${profits}`;
    },
  },
};
</script>

<style></style>
