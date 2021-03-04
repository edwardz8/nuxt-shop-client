<template>
  <main class="container">
    <b-container fluid="md">
      <div class="container-fluid browsing-history">
        <div class="row">
          <div class="col-sm-8 col-8">
            <h1 class="a-size-large a-spacing-none a-text-normal">All Products</h1>

            <b-button variant="primary">Add a New Product</b-button>
            <b-button variant="primary">Add a New Category</b-button>
            <b-button variant="dark">Add a New Owner</b-button>
          </div>
        </div>
      </div>

      <div class="row">
        <b-card v-for="product in products" :key="product._id" class="card">
          <!-- db.myFirstDatabase.renameCollection("vue-node-store") -->

          <!-- Product Image -->
          <a href="#" class="a-link-normal">
            <img :src="product.photo" class="img-fluid" />
          </a>

          <!-- Product Title -->
          <div class="a-spacing-top-base asin-title">
            <span class="a-text-normal">
              <div class="p13n-sc-truncated">{{ product.title }}</div>
            </span>
          </div>

          <!-- Product Rating -->
          <div class="a-row">
            <a href="#">
              <i class="fas fa-star"></i>
              <i class="fas fa-star"></i>
              <i class="fas fa-star"></i>
              <i class="fas fa-star"></i>
              <i class="fas fa-star"></i>
            </a>
            <span class="a-letter-spacing"></span>
            <span class="a-color-tertiary a-size-small asin-reviews">Reviews (1862)</span>
          </div>

          <!-- Product Price -->
          <div class="a-row">
            <span class="a-size-base a-color-price">
              <span class="p13n-sc-price">$ {{ product.price }}</span>
            </span>
          </div>

          <div class="a-row">
            <span class="a-size-base a-color-price">
              <span class="p13n-sc-price">Available: {{ product.stockQuantity }}</span>
            </span>
          </div>

          <!-- Product Button -->
          <div class="a-row button-group">
            <b-button variant="primary">Update</b-button>
            <b-button variant="dark">Delete</b-button>
          </div>
        </b-card>
      </div>
    </b-container>
  </main>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get("http://localhost:8000/api/products");
      console.log(response);
      return {
        products: response.products,
      };
    } catch (err) {}
  },
  data() {
    return {
      products: [],
    };
  },
};
</script>

<style>
.card {
  max-width: 400px;
  margin-left: 1rem;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.row {
  margin-top: 2rem;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
}

.button-group {
  margin-top: 2rem;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}
</style>
