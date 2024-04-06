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

            <img class="card-img-top w-100 d-block" src="/src/assets/img/86-Original-Intense-Blond-Bear-500-ML-murukali-com-1160_1200x1200.jpg" width="259" height="238" alt="Product Image">
            <div class="card-body p-4">
              <p class="text-primary card-text mb-1" style="font-size: smaller;">{{ product.category }}</p>
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
          { 
            id: 1, 
            name: 'Shimmering Sunset Satin', 
            description: 'Sunset satin shimmers with an orange-purple gradient, perfect for elegant dresses', 
            image: 'PXL_20240108_190010108.jpg', 
            price: '$ 10', 
            category: 'GROCERIES' 
          },
          { 
            id: 2, 
            name: 'Bohemian Paisley Cotton Print', 
            description: 'Sunset satin shimmers with an orange-purple gradient, perfect for elegant dresses', 
            image: 'PXL_20240108_190010108.jpg', 
            price: '$ 10', 
            category: 'GROCERIES' 
          },
          {
            id: 3,
            name: 'Umuneke (1 Liter)',
            description: "Traditional Rwandan banana beer. Refreshing taste, unique fermentation. Gluten-free, good probiotics.",
            image: 'umuneke_1l.jpg', 
            price: '$5',
            category: 'BEVERAGES'
          },
          {
            id: 4,
            name: 'Umuneke (500ml)',
            description: "Traditional Rwandan banana beer. Refreshing taste, unique fermentation. Perfect individual serving.",
            image: 'umuneke_500ml.jpg', 
            price: '$3',
            category: 'BEVERAGES'
          },
          {
            id: 5,
            name: 'Umuneke Spiced (750ml)',
            description: "Umuneke with ginger & cloves. Unique flavor experience. Perfect.",
            image: 'umuneke_spiced_750ml.jpg', 
            price: '$6',
            category: 'BEVERAGES'
          },
          {
            id: 5,
            name: 'Umuneke Spiced (750ml)',
            description: "Umuneke with ginger & cloves. Unique flavor experience. Perfect.",
            image: 'umuneke_spiced_750ml.jpg', 
            price: '$6',
            category: 'ELECTONICS'
          }
          
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
  