<template>
  <div>
    <!-- Search Bar -->
    <input type="text" v-model="searchQuery" placeholder="Search products...">
    
    <!-- Category Select -->
    <select v-model="selectedCategory" @change="updateFilteredProducts">
      <option value="">All Categories</option>
      <option v-for="category in categories" :value="category">{{ category }}</option>
    </select>
    
    <!-- Table(s) -->
    <div v-for="(productsInCategory, category) in filteredProducts" :key="category">
      <h2>{{ category }}</h2>
      <table>
        <thead>
          <tr>
            <th>Product Name</th>
            <th>Image</th>
            <th>Price</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="product in productsInCategory" :key="product.id">
            <td>{{ product.name }}</td>
            <td><img :src="product.image" alt="Product Image" style="max-width: 100px;"></td>
            <td>{{ product.price }}</td>
          </tr>
        </tbody>
      </table>
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
      categories: ['AFRICAN FABRICS', 'BEVERAGES', 'COOKING OIL'] 
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



<style scoped>
  .container {
    display: flex;
  }
  
  .category-sidebar {
    width: 30%;
  }
  
  .category-sidebar h2 {
    margin-top: 0;
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
  
  .products-display {
    width: 70%;
  }
  
  .product-row {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }
  
  .product-card {
    flex: 0 0 30%; /* Each card takes 30% width */
    margin-bottom: 20px;
    border: 1px solid #ccc;
    padding: 10px;
  }
  
  .product-card img {
    max-width: 100px;
    margin-right: 10px;
  }
  </style>