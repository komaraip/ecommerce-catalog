<template>
  <div :class="['app-container', containerClass]">
    <div v-if="isLoading" class="loading-container">
      <div class="loading-spinner"></div>
      <p class="loading-text">Loading product...</p>
    </div>

    <div v-else-if="product" :class="['product-card', categoryClass]">
      <template v-if="isClothingProduct">
        <div class="product-image-container">
          <img
            :src="product.image"
            :alt="product.title"
            class="product-image"
          />
        </div>

        <div class="product-details">
          <h1 class="product-title">{{ product.title }}</h1>

          <div class="product-meta">
            <span class="product-category">{{ product.category }}</span>
            <div class="product-rating">
              <span>{{ product.rating.rate }}/5</span>
              <div class="rating-dots">
                <span
                  v-for="n in 5"
                  :key="n"
                  :class="[
                    'rating-dot',
                    {
                      'rating-dot--filled':
                        n <= Math.round(product.rating.rate),
                    },
                  ]"
                ></span>
              </div>
            </div>
          </div>

          <p class="product-description">{{ product.description }}</p>

          <div class="product-price">${{ product.price.toFixed(2) }}</div>

          <div class="product-actions">
            <button class="btn btn--primary">Buy now</button>
            <button class="btn btn--secondary" @click="nextProduct">
              Next product
            </button>
          </div>
        </div>
      </template>

      <template v-else>
        <div class="unavailable-content">
          <div class="sad-face">
            <svg viewBox="0 0 200 150" xmlns="http://www.w3.org/2000/svg">
              <path
                d="M30 40 Q50 25 70 40"
                stroke="#3F3F3F"
                stroke-width="6"
                fill="none"
                stroke-linecap="round"
              />
              <path
                d="M130 40 Q150 25 170 40"
                stroke="#3F3F3F"
                stroke-width="6"
                fill="none"
                stroke-linecap="round"
              />
              <circle cx="50" cy="60" r="10" fill="#3F3F3F" />
              <circle cx="150" cy="60" r="10" fill="#3F3F3F" />
              <path
                d="M40 130 Q100 90 160 130"
                stroke="#3F3F3F"
                stroke-width="6"
                fill="none"
                stroke-linecap="round"
              />
            </svg>
          </div>

          <p class="unavailable-text">This product is unavailable to show</p>
          <button class="unavailable-btn" @click="nextProduct">
            Next product
          </button>
        </div>
      </template>
    </div>

    <div v-else class="product-card product-card--unavailable">
      <div class="unavailable-content">
        <p class="unavailable-text">
          Failed to load product. Please try again.
        </p>
        <button class="unavailable-btn" @click="fetchProduct">Retry</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",

  data() {
    return {
      productIndex: 1,
      product: null,
      isLoading: true,
      maxIndex: 20,
    };
  },

  computed: {
    isClothingProduct() {
      if (!this.product) return false;
      const category = this.product.category.toLowerCase();
      return category === "men's clothing" || category === "women's clothing";
    },

    categoryClass() {
      if (!this.product) return "product-card--unavailable";

      const category = this.product.category.toLowerCase();

      if (category === "men's clothing") {
        return "product-card--men";
      } else if (category === "women's clothing") {
        return "product-card--women";
      } else {
        return "product-card--unavailable";
      }
    },

    containerClass() {
      if (this.isLoading) return "app-container--loading";
      if (!this.product) return "app-container--unavailable";

      const category = this.product.category.toLowerCase();

      if (category === "men's clothing") {
        return "app-container--men";
      } else if (category === "women's clothing") {
        return "app-container--women";
      } else {
        return "app-container--unavailable";
      }
    },
  },

  methods: {
    async fetchProduct() {
      this.isLoading = true;

      try {
        const response = await fetch(
          `https://fakestoreapi.com/products/${this.productIndex}`
        );

        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }

        this.product = await response.json();
      } catch (error) {
        console.error("Failed to fetch product:", error);
        this.product = null;
      } finally {
        this.isLoading = false;
      }
    },

    nextProduct() {
      this.productIndex++;

      if (this.productIndex > this.maxIndex) {
        this.productIndex = 1;
      }

      this.fetchProduct();
    },
  },

  mounted() {
    this.fetchProduct();
  },
};
</script>

<style scoped></style>
