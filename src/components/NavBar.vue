<!-- Vue Component Template -->
<template>
  <div>
    <!-- Search Bar -->
    <input type="text" v-model="searchQuery" placeholder="Search products...">
    
    <!-- Table -->
    <table>
      <thead>
        <tr>
          <th>Product Name</th>
          <th>Image</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in filteredProducts" :key="product.id">
          <td>{{ product.name }}</td>
          <td><img :src="product.image" alt="Product Image" style="max-width: 100px;"></td>
          <td>{{ product.price }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
      products: [ // Sample product data
        { id: 1, name: 'Product 1', image: 'image1.jpg', price: '$10' },
        { id: 2, name: 'Product 2', image: 'image2.jpg', price: '$20' },
        { id: 3, name: 'Product 3', image: 'image3.jpg', price: '$30' },
        // Add more products as needed
      ]
    };
  },
  computed: {
    filteredProducts() {
      // Filter products based on search query
      return this.products.filter(product =>
        product.name.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    }
  }
};
</script>

<style scoped>
/* Add your component-specific styles here */
</style>
