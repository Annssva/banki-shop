<template>
  <div class="app">
    <AppHeader
      :search-query="searchQuery"
      @search="handleSearch"
    />

    <main class="main container">
      <ProductList
        :products="filteredProducts"
      />
    </main>

    <AppFooter />
  </div>
</template>

<script>
import products from '@/data/products'

import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import ProductList from './components/ProductList.vue'

export default {
  name: 'App',

  components: {
    AppHeader,
    AppFooter,
    ProductList
  },

  data() {
    return {
      products,
      searchQuery: ''
    }
  },

  computed: {
    filteredProducts() {
      const query = this.searchQuery.trim().toLowerCase()

      if (!query) {
        return this.products
      }

      return this.products.filter(product => {
        const search = `${product.title} ${product.author}`.toLowerCase()

        return search.includes(query)
      })
    }
  },

  methods: {
    handleSearch(value) {
      this.searchQuery = value
    }
  }
}
</script>

<style>
</style>
