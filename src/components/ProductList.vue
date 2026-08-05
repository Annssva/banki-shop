<template>
  <section class="products">
    <h1 class="products__title">
      Картины эпохи Возрождения
    </h1>

    <transition-group
        name="products"
        tag="div"
        class="products__list"
    >
      <ProductCard
        v-for="product in products"
        :key="product.id"
        :product="product"
        @buy="$emit('buy', $event)"
      />
    </transition-group>
  </section>
</template>

<script>
import ProductCard from './ProductCard.vue'

export default {
  name: 'ProductList',

  components: {
    ProductCard
  },

  props: {
    products: {
      type: Array,
      required: true
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
    position: relative;
    display: flex;
    flex-wrap: wrap;

    gap: 32px;

    overflow: hidden;
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

.products-enter-active,
.products-leave-active {
  transition:
    opacity .3s ease,
    transform .3s ease;
}

.products-move {
  transition: transform .45s cubic-bezier(.22, 1, .36, 1);
}

.products-enter {
  opacity: 0;
  transform: translateY(10px);
}

.products-leave-to {
  opacity: 0;
  transform: scale(.96);
}

.products-leave-active {
  position: absolute;
  pointer-events: none;
}
</style>