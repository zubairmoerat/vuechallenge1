<template>
  <div class="wrapper">
    <div>
      <input type="text" v-model="searchedProduct" placeholder="Search" @input="filtered" />
    </div>
    <div>
      <label for="category">Select Category:</label>
      <select v-model="selectingCategory" @change="filtered">
        <option v-for="category in categories" :key="category" :value="category">
          {{ category }}
        </option>
      </select>
    </div>
    <div class="row" v-if="filteredProducts.length">
      <div class="prodCard" v-for="product in filteredProducts" :key="product.id">
        <div class="prodCard-img">
          <img :src="product.image" :alt="product.name" />
        </div>
        <div class="prodcard-info">
          <h3>{{ product.name }}</h3>
          <p>{{ product.amount }}</p>
        </div>
      </div>
    </div>
    <div class="row" v-else>
      <p>Sorry, No Products in Stock</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'Gymbag',
          image: 'https://i.postimg.cc/sgmsbVPP/js-EOMP-prod2.jpg',
          amount: 500,
          category: 'Equipment',
        },
        {
          id: 2,
          name: 'Lifting Belt',
          image: 'https://i.postimg.cc/J4H7FVtt/js-EOMP-prod3.jpg',
          amount: 1500,
          category: 'Equipment',
        },
        {
          id: 3,
          name: 'Protein Powder',
          image: 'https://i.postimg.cc/RhfYmFwP/js-EOMP-prod1.jpg',
          amount: 1000,
          category: 'Nutrition', 
        },
        {
          id: 4,
          name: 'Trenbolone',
          image: 'https://i.postimg.cc/RFQ1Cdrk/js-EOMP-prod6.jpg',
          amount: 5000,
          category: 'Nutrition', 
        }
      ],
      categories: ['Nutrition', 'Equipment'],
      selectingCategory: 'Nutrition',
      searchedProduct: '',
    };
  },
  computed: {
    filteredProducts() {
      let filter = this.products;
      if (this.selectingCategory !== 'Nutrition') {
        filter = filter.filter(product => product.category === this.selectingCategory);
      }
      if (this.searchedProduct.trim() !== '') {
        const searchItem = this.searchedProduct.toLowerCase();
        filter = filter.filter(product => product.name.toLowerCase().includes(searchItem));
      }
      return filter;
    },
  },
  methods: {},
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
