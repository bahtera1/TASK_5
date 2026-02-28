<template>
  <div id="app" :class="sectionClass">
    <!-- Loading -->
    <div v-if="isLoading" class="skeleton-card">
      <div class="skeleton-image skeleton-pulse"></div>
      <div class="skeleton-details">
        <div class="skeleton-title skeleton-pulse"></div>
        <div class="skeleton-meta skeleton-pulse"></div>
        <div class="skeleton-desc skeleton-pulse"></div>
        <div class="skeleton-desc short skeleton-pulse"></div>
        <div class="skeleton-price skeleton-pulse"></div>
        <div class="skeleton-buttons">
          <div class="skeleton-btn skeleton-pulse"></div>
          <div class="skeleton-btn skeleton-pulse"></div>
        </div>
      </div>
    </div>
    <!-- ProductDisplay -->
    <ProductDisplay v-else :product="product" @next="nextProduct" />
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";

export default {
  name: "App",

  components: {
    ProductDisplay,
  },

  data() {
    return {
      productIndex: 1,
      product: null,
      category: "",
      isLoading: false,
    };
  },

  computed: {
    sectionClass() {
      if (this.category === "men's clothing") return "men-section";
      if (this.category === "women's clothing") return "women-section";
      return "unavailable-section";
    },
  },
  methods: {
    async fetchProduct() {
      this.isLoading = true;

      try {
        const response = await fetch(
          `https://fakestoreapi.com/products/${this.productIndex}`,
        );
        const data = await response.json();

        this.category = data.category;

        if (
          data.category === "men's clothing" ||
          data.category === "women's clothing"
        ) {
          this.product = data;
        } else {
          this.product = null;
        }
      } catch (error) {
        console.error("Gagal fetch API:", error);
        this.product = null;
      }

      this.isLoading = false;
    },
    nextProduct() {
      this.productIndex++;
      if (this.productIndex > 20) {
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
