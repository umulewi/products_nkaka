<template>
    <div class="container py-4 py-xl-5">
      <div class="row" style="margin-bottom: 13px;">
        <div class="col-xl-6 offset-xl-6 text-end">
          <form>
            <select v-model="selectedCategory" class="form-select d-inline-block" style="min-width: auto; max-width: 240px; margin-left: 0; margin-right: 7px;">
              <option value="" selected>Choose Category</option>
              <option v-for="category in categories" :key="category">{{ category }}</option>
            </select>
            <input v-model="searchQuery" class="form-control d-inline-block" type="search" placeholder="Search products" style="max-width: 257px;">
          </form>
        </div>
      </div>
  
      <div class="row gy-4">
        <div class="col-xl-3 col-lg-4 col-md-6" v-for="product in filteredProducts" :key="product.id">
          <div class="card">
            <img class="card-img-top w-100 d-block" :src="product.image" width="259" height="238" alt="Product Image">
            <div class="card-body p-4" style="height: 226.2px;">
              <p class="text-primary card-text mb-0">{{ product.category }}</p>
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">{{ product.description }}</p>
              <h6 class="card-title">{{ product.price }}</h6>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchQuery: '',
        selectedCategory: '',
        products: [
          // Sample product data
          { id: 1, name: 'banana', description: 'shjsjsjsjs', image: 'PXL_20240108_190010108.jpg', price: '$10', category: 'AFRICAN FABRICS' },
          { id: 2, name: 'umuneke', description: 'shjsjsjsjs', image: 'PXL_20240108_190010108.jpg', price: '$10', category: 'BEVERAGES' },
          { id: 3, name: 'umuneke', description: 'shjsjsjsjs', image: 'PXL_20240108_190010108.jpg', price: '$10', category: 'BEVERAGES' },
          { id: 3, name: 'umuneke', description: 'shjsjsjsjs', image: 'PXL_20240108_190010108.jpg', price: '$10', category: 'BEVERAGES' },
          { id: 3, name: 'umuneke', description: 'shjsjsjsjs', image: 'PXL_20240108_190010108.jpg', price: '$10', category: 'BEVERAGES' },
          // Add more products as needed
        ],
        categories: ['AFRICAN FABRICS', 'BEVERAGES', 'COOKING OIL', 'gggggg']
      };
    },
    computed: {
      filteredProducts() {
        let filtered = this.products;
        if (this.selectedCategory) {
          filtered = filtered.filter(product => product.category === this.selectedCategory);
        }
        if (this.searchQuery) {
          const query = this.searchQuery.toLowerCase();
          filtered = filtered.filter(product => product.name.toLowerCase().includes(query) || product.description.toLowerCase().includes(query));
        }
        return filtered;
      }
    }
  };
  </script>
  
  <style scoped>
  .fit-cover {
    object-fit: cover;
  }
  </style>
  