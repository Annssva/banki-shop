<template>
  <div class="app">
    <AppHeader />

    <div class="main container">
      <ProductList />
    </div>

    <AppFooter />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import ProductList from './components/ProductList.vue'

export default {
  name: 'App',

  components: {
    AppHeader,
    AppFooter,
    ProductList
  }
}
</script>

<style>
</style>
