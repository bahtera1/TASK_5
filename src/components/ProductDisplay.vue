<script>
export default {
  name: "ProductDisplay",

  props: {
    product: {
      type: Object,
      default: null,
    },
  },
  methods: {
    onNext() {
      this.$emit("next");
    },
  },
};
</script>

<template>
  <div>
    <div v-if="product" class="product-card">
      <div class="product-image">
        <img :src="product.image" :alt="product.title" />
      </div>

      <div class="product-details">
        <h1 class="product-title">{{ product.title }}</h1>

        <div class="divider"></div>

        <div class="product-meta">
          <span class="product-category">{{ product.category }}</span>
          <div class="product-rating">
            <span class="rating-number">{{ product.rating.rate }}/5</span>
            <span
              v-for="dot in 5"
              :key="dot"
              class="dot"
              :class="dot <= Math.round(product.rating.rate) ? 'filled' : 'empty'"
            ></span>
          </div>
        </div>

        <p class="product-description">{{ product.description }}</p>

        <div class="divider"></div>

        <h2 class="product-price">${{ product.price.toFixed(2) }}</h2>

        <div class="product-actions">
          <button class="btn-buy">Buy now</button>
          <button class="btn-next" @click="onNext">Next product</button>
        </div>
      </div>
    </div>

    <div v-else class="unavailable-container">
      <div class="sad-face">
        <div class="face">
          <div class="eyes">
            <span class="eye"></span>
            <span class="eye"></span>
          </div>
          <div class="mouth"></div>
        </div>
      </div>
      <p class="unavailable-text">This product is unavailable to show</p>
      <button class="btn-next-unavailable" @click="onNext">Next product</button>
    </div>
  </div>
</template>

<style scoped>
.product-card {
  display: flex;
  background: var(--white);
  border-radius: 12px;
  overflow: hidden;
  max-width: 900px;
  width: 90%;
  min-height: 400px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  transition: all 0.3s ease;
}

.product-card:hover {
  box-shadow: 0 15px 50px rgba(0, 0, 0, 0.25);
  transform: translateY(-5px);
}

.product-image {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 30px;
  background: var(--white);
}

.product-image img {
  max-width: 100%;
  max-height: 350px;
  object-fit: contain;
}

.product-details {
  flex: 1;
  padding: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.product-title {
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--dark);
  margin: 0 0 12px 0;
}

.divider {
  width: 100%;
  height: 1px;
  background: #e0e0e0;
  margin: 8px 0;
}

.product-meta {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 10px 0 15px 0;
}

.product-category {
  font-size: 0.85rem;
  color: #666;
  text-transform: capitalize;
}

.product-rating {
  display: flex;
  align-items: center;
  gap: 4px;
}

.rating-number {
  font-size: 0.85rem;
  color: #666;
  margin-right: 4px;
}

.dot {
  width: 14px;
  height: 14px;
  border-radius: 50%;
  display: inline-block;
}

.dot.filled {
  background: var(--dark);
}

.dot.empty {
  background: transparent;
  border: 2px solid #ccc;
}

.product-description {
  font-size: 0.9rem;
  color: #555;
  line-height: 1.6;
  margin-bottom: 15px;
  display: -webkit-box;
  -webkit-line-clamp: 5;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.product-price {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--dark);
  margin: 10px 0 20px 0;
}

.product-actions {
  display: flex;
  gap: 12px;
}

.btn-buy,
.btn-next {
  flex: 1;
  padding: 12px 28px;
  border-radius: 8px;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-buy {
  border: none;
}

.btn-next {
  background: transparent;
}

.btn-buy:hover,
.btn-next:hover {
  opacity: 0.85;
  transform: translateY(-2px);
}

.unavailable-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 80vh;
  color: var(--white);
  text-align: center;
  padding: 20px;
}

.sad-face {
  margin-bottom: 30px;
}

.face {
  width: 150px;
  height: 150px;
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-radius: 50%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.eyes {
  display: flex;
  gap: 30px;
  margin-bottom: 15px;
}

.eye {
  width: 18px;
  height: 18px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 50%;
}

.mouth {
  width: 50px;
  height: 25px;
  border: 3px solid rgba(255, 255, 255, 0.5);
  border-radius: 0 0 50px 50px;
  border-top: none;
  transform: rotate(180deg);
}

.unavailable-text {
  font-size: 1.3rem;
  font-weight: 500;
  margin-bottom: 30px;
  color: rgba(255, 255, 255, 0.9);
}

.btn-next-unavailable {
  padding: 12px 36px;
  background: transparent;
  color: var(--white);
  border: 2px solid var(--white);
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-next-unavailable:hover {
  background: rgba(255, 255, 255, 0.1);
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .product-card {
    flex-direction: column;
  }
  .product-image img {
    max-height: 250px;
  }
}
</style>
