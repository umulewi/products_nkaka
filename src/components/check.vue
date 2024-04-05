<template>
    <div class="container">
      <!-- Category Sidebar -->
      <div class="category-sidebar">
        <h2>Categories</h2>
        <ul>
          <li v-for="category in categories" :key="category" @click="selectCategory(category)">
            {{ category }}
          </li>
        </ul>
      </div>
      
      <!-- Products Display - Only show when a category is selected -->
      <div class="products-display" v-if="selectedCategory">
        <h2>{{ selectedCategory }}</h2>
        <div class="product-row" v-for="(product, index) in filteredProducts" :key="index">
          <div class="product-card" v-for="productItem in product" :key="productItem.id">
            <img :src="productItem.image" alt="Product Image" style="max-width: 100px;">
            <div>
              <h3>{{ productItem.name }}</h3>
              <p>{{ productItem.price }}</p>
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
        selectedCategory: null,
        products: [
          // Sample product data
          { id: 1, name: 'banana', image: 'image1.jpg', price: '$10', category: 'AFRICAN FABRICS' },
          { id: 1, name: 'banana', image: 'image1.jpg', price: '$10', category: 'AFRICAN FABRICS' },
          { id: 1, name: 'banana', image: 'image1.jpg', price: '$10', category: 'AFRICAN FABRICS' },
          { id: 1, name: 'banana', image: 'image1.jpg', price: '$10', category: 'AFRICAN FABRICS' },
          { id: 1, name: 'banana', image: 'image1.jpg', price: '$10', category: 'AFRICAN FABRICS' },
          { id: 1, name: 'banana', image: 'image1.jpg', price: '$10', category: 'AFRICAN FABRICS' },
          { id: 2, name: 'mango', image: 'image2.jpg', price: '$20', category: 'COOKING OIL' },
          { id: 3, name: 'banana2', image: 'image3.jpg', price: '$30', category: 'AFRICAN FABRICS' },
          { id: 4, name: 'Product 4', image: 'image4.jpg', price: '$30', category: 'Category C' }
          // Add more products as needed
        ],
        categories: ['AFRICAN FABRICS', 'BEVERAGES', 'COOKING OIL','gggggg'] 
      };
    },
    computed: {
      filteredProducts() {
        let filtered = {};
        if (this.selectedCategory) {
          filtered = this.products.filter(product => product.category === this.selectedCategory);
        } else {
          filtered = this.products;
        }
        return this.chunkArray(filtered, 3); // Split products into chunks of three
      }
    },
    methods: {
      selectCategory(category) {
        this.selectedCategory = category;
      },
      // Function to split array into chunks
      chunkArray(array, size) {
        const chunkedArray = [];
        for (let i = 0; i < array.length; i += size) {
          chunkedArray.push(array.slice(i, i + size));
        }
        return chunkedArray;
      }
    }
  };
  </script>
  
  