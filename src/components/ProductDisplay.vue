<script></script>
<template>
  <div>
    <!-- CARD PRODUK — tampil jika product ada -->
    <div v-if="product" class="product-card">
      <!-- Gambar (kiri) -->
      <div class="product-image">
        <img :src="product.image" :alt="product.title" />
      </div>

      <!-- Detail (kanan) -->
      <div class="product-details">
        <h1 class="product-title">{{ product.title }}</h1>

        <div class="product-meta">
          <span class="product-category">{{ product.category }}</span>
          <div class="product-rating">
            <span v-for="star in 5" :key="star" class="star">
              {{ star <= Math.round(product.rating.rate) ? "★" : "☆" }}
            </span>
            <span class="rating-count">({{ product.rating.count }})</span>
          </div>
        </div>

        <p class="product-description">{{ product.description }}</p>
        <h2 class="product-price">${{ product.price.toFixed(2) }}</h2>

        <div class="product-actions">
          <button class="btn-buy">Buy now</button>
          <button class="btn-next" @click="onNext">Next product</button>
        </div>
      </div>
    </div>

    <!-- UNAVAILABLE — tampil jika product = null -->
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

<style></style>
