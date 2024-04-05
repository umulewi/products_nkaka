<template>
    <div>
      <!-- Category Sidebar -->
      <div class="category-sidebar">
        <h2>Categories</h2>
        <ul>
          <li v-for="category in categories" :key="category" @click="selectCategory(category)">
            {{ category }}
          </li>
        </ul>
      </div>
      
      <!-- Products Display -->
      <div class="products-display">
        <h2 v-if="selectedCategory">{{ selectedCategory }}</h2>
        <div class="product-card" v-for="product in filteredProducts" :key="product.id">
          <img :src="product.image" alt="Product Image" style="max-width: 100px;">
          <div>
            <h3>{{ product.name }}</h3>
            <p>{{ product.price }}</p>
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
        selectedCategory: null,
        products: [
          // Sample product data
          { id: 1, name: 'banana', image: 'image1.jpg', price: '$10', category: 'Category A' },
          { id: 2, name: 'mango', image: 'image2.jpg', price: '$20', category: 'Category B' },
          { id: 3, name: 'banana2', image: 'image3.jpg', price: '$30', category: 'Category A' },
          { id: 4, name: 'Product 4', image: 'image4.jpg', price: '$30', category: 'Category C' }
          // Add more products as needed
        ],
        categories: ['Category A', 'Category B', 'Category C'] 
      };
    },
    computed: {
      filteredProducts() {
        return this.products.filter(product =>
          product.name.toLowerCase().includes(this.searchQuery.toLowerCase()) &&
          (this.selectedCategory ? product.category === this.selectedCategory : true)
        );
      }
    },
    methods: {
      selectCategory(category) {
        this.selectedCategory = category;
      }
    }
  };
  </script>
  
  <style scoped>
  .category-sidebar {
    float: left;
    width: 30%;
  }
  
  .products-display {
    float: right;
    width: 70%;
  }
  
  .category-sidebar ul {
    list-style: none;
    padding: 0;
  }
  
  .category-sidebar ul li {
    cursor: pointer;
    padding: 5px;
    border-bottom: 1px solid #ccc;
  }
  
  .category-sidebar ul li:hover {
    background-color: #f0f0f0;
  }
  
  .product-card {
    display: flex;
    align-items: center;
    padding: 10px;
    border: 1px solid #ccc;
    margin: 5px;
  }
  
  .product-card img {
    max-width: 100px;
    margin-right: 10px;
  }
  </style>
  