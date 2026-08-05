<template>
  <div class="app">
    <AppHeader :search-query="searchQuery" @search="handleSearch" />

    <main class="main container">
      <ProductList :products="filteredProducts" @buy="buyProduct" @open="openProduct" />

      <ProductModal
        v-if="selectedProduct"
        :product="selectedProduct"
        @close="selectedProduct = null"
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
import ProductModal from './components/ProductModal.vue'

export default {
  name: 'App',

  components: {
    AppHeader,
    AppFooter,
    ProductList,
    ProductModal
  },

  data() {
    return {
      products,
      searchQuery: '',
      storageKey: 'banki-shop-cart',
      selectedProduct: null
    }
  },

  mounted() {
    this.loadPurchasedProducts()
  },

  computed: {
    filteredProducts() {
      const query = this.searchQuery.trim().toLowerCase()

      if (!query) {
        return this.products
      }

      return this.products.filter(product =>
          product.title.toLowerCase().includes(query)
      )
    }
  },

  methods: {
    handleSearch(value) {
      this.searchQuery = value
    },

    buyProduct(id) {
      const product = this.products.find((item) => item.id === id)

      if (!product || product.purchaseState !== 'idle') {
        return
      }

      product.purchaseState = 'processing'

      setTimeout(() => {
        product.purchaseState = 'cart'

        this.savePurchasedProducts()
      }, 2000)
    },

    loadPurchasedProducts() {
      const savedProducts = JSON.parse(localStorage.getItem(this.storageKey))

      if (!savedProducts) {
        return
      }

      this.products.forEach((product) => {
        if (savedProducts.includes(product.id)) {
          product.purchaseState = 'cart'
        }
      })
    },

    savePurchasedProducts() {
      const purchasedProducts = this.products
        .filter((product) => product.purchaseState === 'cart')
        .map((product) => product.id)

      localStorage.setItem(this.storageKey, JSON.stringify(purchasedProducts))
    },
    openProduct(product) {
      this.selectedProduct = product
    }
  }
}
</script>

<style></style>
