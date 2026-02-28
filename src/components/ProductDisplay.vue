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
        <img :src="product.image" :alt="product.title" loading="lazy" />
      </div>

      <div class="product-details">
        <h1 class="product-title">{{ product.title }}</h1>

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

        <div class="divider"></div>

        <p class="product-description">{{ product.description }}</p>

        <div class="divider"></div>

        <h2 class="product-price">${{ product.price.toFixed(2) }}</h2>

        <div class="product-actions">
          <button class="btn-buy">Buy now</button>
          <button class="btn-next" @click="onNext">Next product</button>
        </div>
      </div>
    </div>

    <div v-else class="unavailable-card">
      <div class="unavailable-face">
        <svg viewBox="0 0 200 160" xmlns="http://www.w3.org/2000/svg">
          <path d="M50 30 Q65 15 80 35" stroke="#1e1e1e" stroke-width="4" fill="none" stroke-linecap="round"/>
          <path d="M120 30 Q135 15 150 35" stroke="#1e1e1e" stroke-width="4" fill="none" stroke-linecap="round"/>
          <path d="M55 55 Q65 70 75 55" stroke="#1e1e1e" stroke-width="4" fill="none" stroke-linecap="round"/>
          <path d="M125 55 Q135 70 145 55" stroke="#1e1e1e" stroke-width="4" fill="none" stroke-linecap="round"/>
          <path d="M40 120 Q100 80 160 120" stroke="#1e1e1e" stroke-width="5" fill="none" stroke-linecap="round"/>
        </svg>
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
  flex: 2;
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
  flex: 3;
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

.unavailable-card {
  background: var(--white);
  border-radius: 12px;
  max-width: 900px;
  width: 90vw;
  min-height: 400px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 40px;
  text-align: center;
}

.unavailable-face svg {
  width: 200px;
  height: 160px;
  margin-bottom: 20px;
}

.unavailable-text {
  font-size: 1.1rem;
  font-weight: 400;
  color: var(--dark);
  margin-bottom: 20px;
}

.btn-next-unavailable {
  padding: 12px 50px;
  background: transparent;
  color: var(--dark);
  border: 2px solid var(--dark);
  border-radius: 4px;
  font-size: 0.95rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-next-unavailable:hover {
  background: rgba(0, 0, 0, 0.05);
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
