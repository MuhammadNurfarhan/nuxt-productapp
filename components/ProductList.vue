<template>
    <div>
      <input v-model="searchQuery" placeholder="Cari produk..." @input="filterProducts" />
  
      <div v-if="isLoading" class="loading">Loading...</div>
  
      <div v-else-if="filteredProducts.length === 0">Tidak ada produk yang ditemukan.</div>
  
      <div v-else class="product-grid">
        <div v-for="product in filteredProducts" :key="product.id" class="product-card">
          <img :src="product.image" alt="product.title" class="product-image" />
          <h3>{{ product.title }}</h3>
          <p>{{ product.price }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [],
        searchQuery: '',
        filteredProducts: [],
        isLoading: true
      };
    },
    async created() {
      try {
        const response = await fetch('https://fakestoreapi.com/products');
        this.products = await response.json();
        this.filteredProducts = this.products;
      } catch (error) {
        console.error('Error fetching products:', error);
      } finally {
        this.isLoading = false;
      }
    },
    methods: {
      filterProducts() {
        const query = this.searchQuery.toLowerCase();
        this.filteredProducts = this.products.filter(product =>
          product.title.toLowerCase().includes(query)
        );
      },
    },
  };
  </script>
  
  <style scoped>
  .product-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
  }
  
  .product-card {
    border: 1px solid #ddd;
    border-radius: 10px;
    padding: 10px;
    width: 200px;
  }
  
  .product-image {
    width: 100%;
    height: auto;
  }
  
  input {
    display: block;
    margin: 0 auto 20px;
    padding: 10px;
    width: 80%;
    max-width: 400px;
    font-size: 16px;
  }

  .loading {
    text-align: center;
    font-size: 18px;
    color: #555;
  }
  </style>
  