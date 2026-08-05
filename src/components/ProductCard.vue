<template>
  <article
    class="card"
    :class="{ 'card--sold': product.status === 'sold' }"
    >

    <img
      :src="product.images[0]"
      :alt="product.title"
      class="card__image"
      @click="$emit('open', product)"
    />

    <div class="card__content">

    <h2
        class="card__title"
        @click="$emit('open', product)"
    >
        {{ product.title }}
        <br>
        {{ product.author }}
      </h2>


      <div
        v-if="product.status !== 'sold'"
        class="card__bottom"
      >
        <div class="card__prices">

            <span
                v-if="product.oldPrice"
                class="card__old-price"
            >
                {{ formatPrice(product.oldPrice) }} $
            </span>

            <span class="card__price">
                {{ formatPrice(product.price) }} $
            </span>
        </div>


        <button
            class="card__button"
            :class="{
                'card__button--processing': product.purchaseState === 'processing',
                'card__button--cart': product.purchaseState === 'cart'
            }"
            :disabled="product.purchaseState !== 'idle'"
            @click="$emit('buy', product.id)"
        >
            <img
                v-if="product.purchaseState === 'cart'"
                :src="checkIcon"
                alt=""
                class="card__button-icon"
            />

            <span>
                {{ buttonText }}
            </span>
        </button>
      </div>


        <div
            v-else
            class="card__sold"
        >
            Продана на аукционе
        </div>
    </div>

  </article>
</template>


<script>
import checkIcon from '@/assets/icons/feather_check.svg'

export default {
  name: 'ProductCard',

  props: {
    product: {
      type: Object,
      required: true
    }
  },

  computed: {
    buttonText() {
        switch (this.product.purchaseState) {
        case 'processing':
            return 'Обрабатывается'

        case 'cart':
            return 'В корзине'

        default:
            return 'Купить'
        }
    }
  },

    data() {
        return {
            checkIcon
        }
    },

  methods: {
    formatPrice(value) {
      return value
        .toLocaleString('ru-RU')
    }
  }
}
</script>


<style lang="scss">
.card {
  width: 280px;
  height: 328px;

  display: flex;
  flex-direction: column;
  border: 1px solid #E1E1E1;

  flex-shrink: 0;

  background: transparent;

  &--sold {
    opacity: 0.5;
  }


  &__image {
    width: 100%;
    height: 158px;

    display: block;

    object-fit: cover;
    cursor: pointer;
    transition: transform $transition;

    &:hover {
        transform: scale(1.02);
    }
  }


  &__content {
    flex: 1;
    border-top: 1px solid #E1E1E1;

    display: flex;
    flex-direction: column;
    justify-content: space-between;

    padding: 20px 23px 22px 23px;
}


  &__title {
    margin: 0;

    color: $text-color;

    font-size: 18px;
    font-weight: 400;
    line-height: 150%;
    cursor: pointer;

    transition: color $transition;

    &:hover {
        color: #191717;

    }
  }


  &__bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;

    margin-top: 20px;

    gap: 8px;
  }


  &__prices {
    display: flex;
    flex-direction: column;
  }


  &__old-price {
    color: #A0A0A0;

    font-size: 14px;
    font-weight: 300;
    line-height: 150%;

    font-family: inherit;
    vertical-align: middle;
    text-decoration: line-through;
  }


  &__price {
    color: $text-color;

    font-size: 16px;
    font-weight: 700;
    line-height: 150%;
    white-space: nowrap;
  }


  &__button {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 4px;
    width: fit-content;
    min-width: 118px;
    height: 48px;
    padding: 0 8px;

    border: none;

    background: $accent-color;

    color: #fff;

    font-family: inherit;
    font-size: 14px;
    font-weight: 700;
    line-height: 150%;

    cursor: pointer;

    transition: background $transition;


    &:hover {
      background: $hover-color;
    }


    &:active {
      background: $activate-color;

        &:hover {
            background: $activate-color;
        }
    }


    &:disabled {
      pointer-events: none;
    }

    &--processing {
        font-size: 13px;
        background: $disabled-color;

        &:hover {
            background: $disabled-color;
        }
    }

    &--cart {
        background: $activate-color;

        &:hover {
            background: $activate-color;
        }
    }
  }

    &__sold {
        margin-top: auto;
        margin-bottom: 12px;

        color: $text-color;

        font-size: 16px;
        font-weight: 700;
        line-height: 150%;
        vertical-align: middle;
    }

    &__button-icon {
        width: 16px;
        height: 16px;

        flex-shrink: 0;
    }
}
</style>