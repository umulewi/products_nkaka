 <template>
    <div class="container py-4 py-xl-5">
      <div class="row" style="margin-bottom: 13px;">
        <div class="col-xl-6 offset-xl-6 text-end">
          <form>
            <select v-model="selectedCategory" class="form-select d-inline-block" style="min-width: auto; max-width: 240px; margin-left: 0; margin-right: 7px;">
              <option value="" selected>All Products</option>
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
            <div class="card-body p-4">
              <p class="text-primary card-text mb-1" style="font-size: smaller;">{{ product.category }}</p>
              <h5 class="card-title">{{ product.name }}</h5>
              <p class="card-text">{{ product.description }}</p>
              <h6 class="card-title">$ {{ product.price }}</h6>
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
          { 
            id: 1, 
            name: 'Intense Blond Bear', 
            description: 'A full-bodied red wine, likely made from Merlot grapes. Merlot is known for its smooth taste and dark fruit.', 
            image: '/src/assets/img/86-Original-Intense-Blond-Bear-500-ML-murukali-com-1160_1200x1200.jpg', 
            price: '3.5', 
            category: 'BEVERAGES' 
          },
          { 
            id: 2, 
            name: 'Grand Sud Merlot', 
            description: 'A full-bodied red wine, likely made from Merlot grapes. Merlot is known for its smooth taste and dark fruits.', 
            image: '/src/assets/img/Grand-Sud-Merlot-1L-pc-murukali-com-7668_1200x1200.jpg', 
            price: '32.0', 
            category: 'BEVERAGES' 
          },
          {
            id: 3,
            name: 'Inyange chocolate milk',
            description: "Rich and creamy chocolate flavored milk, perfect for a delicious treat. Enjoy it chilled for a refreshing drink.",
            image: '/src/assets/img/Inyange-chocolate-milk-1L-murukali-com-2512_1200x1200.jpg', 
            price: '1.34',
            category: 'BEVERAGES'
          },
          {
            id: 4,
            name: 'Inyange Low Fat Milk',
            description: "All the goodness of milk with less fat. Great for those watching their calorie intake or who prefer a lighter taste. ",
            image: '/src/assets/img/Inyange-Low-Fat-Milk-L-murukali-com-8860_1200x1200.jpg', 
            price: '1.89',
            category: 'BEVERAGES'
          },
          {
            id: 4,
            name: 'Green Pepper',
            description: " These crisp, emerald-green vegetables are not only delicious but also packed with essential vitamins.",
            image: '/src/assets/img/greenpepper.jpg', 
            price: '1.2',
            category: 'GROCERIES'
          },
          {
            id: 5,
            name: 'Parsley',
            description: "This vibrant green herb is a kitchen essential, adding a touch of brightness and freshness to any ",
            image: '/src/assets/img/sereri.jpg', 
            price: '0.32',
            category: 'GROCERIES'
          },
          {
            id: 5,
            name: 'Eggplant',
            description: "Beautiful, purple vegetables offering a mild, slightly sweet flavor that complements countless dishes.",
            image: '/src/assets/img/Eggplant.jpg', 
            price: '0.32',
            category: 'GROCERIES'
          },
          {
            id: 5,
            name: 'Epinard',
            description: "These tender, young spinach leaves are bursting with flavor and nutrients, making them a perfect addition to any meal.",
            image: '/src/assets/img/Epinard-bunch-murukali-com-1726_1200x1200.jpg', 
            price: '0.32',
            category: 'GROCERIES'
          },
          
        ],
        categories: ['GROCERIES', 'BEVERAGES', 'ELECTONICS']
        
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
  