<template>
  <section class="products">
    <h1 class="products__title">
      Картины эпохи Возрождения
    </h1>

    <div class="products__list">
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :product="product"
      />
    </div>
  </section>
</template>

<script>
import products from '@/data/products'
import ProductCard from './ProductCard.vue'

export default {
  name: 'ProductList',

  components: {
    ProductCard
  },

  data() {
    return {
      products
    }
  }
}
</script>

<style lang="scss">
.products {
  padding-top: 45px;

  &__title {
    margin: 0 0 37px;

    color: $text-color;

    font-size: 24px;
    font-weight: 700;
    line-height: 150%;
  }

  &__list {
    display: flex;
    flex-wrap: nowrap;

    gap: 32px;

    overflow-x: auto;
  }
}

@media (max-width: 768px) {
  .products {
    padding-top: 32px;

    &__title {
      font-size: 22px;
    }

    &__list {
      gap: 24px;
    }
  }
}
</style>