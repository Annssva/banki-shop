<template>
  <transition
    name="modal"
    appear
  >
    <div
      v-if="product"
      class="modal"
      @click.self="$emit('close')"
    >

      <div class="modal__window">

        <button
          class="modal__close"
          @click="$emit('close')"
        >
          ×
        </button>


        <div class="modal__slider">

          <transition :name="slideDirection">
            <img
                :key="currentImage"
                :src="currentImage"
                :alt="product.title"
                class="modal__image"
            />
          </transition>


          <div
            v-if="product.images.length > 1"
            class="modal__controls"
          >

            <button
              class="modal__arrow"
              @click="prevImage"
            >
              ←
            </button>

            <button
              class="modal__arrow"
              @click="nextImage"
            >
              →
            </button>

          </div>

        </div>


        <div class="modal__content">

          <h2 class="modal__title">
            {{ product.title }}
            <br>
            {{ product.author }}
          </h2>


          <p class="modal__description">
            {{ product.description }}
          </p>


          <div
            v-if="product.status !== 'sold'"
            class="modal__price"
          >
            {{ formatPrice(product.price) }} $
          </div>


          <div
            v-else
            class="modal__sold"
          >
            Продана на аукционе
          </div>

        </div>

      </div>

    </div>
  </transition>
</template>


<script>
export default {
  name: 'ProductModal',

  props: {
    product: {
      type: Object,
      default: null
    }
  },

  data() {
    return {
      currentIndex: 0,
      slideDirection: 'slide-next'
    }
  },

  computed: {
    currentImage() {
      return this.product.images[this.currentIndex]
    }
  },

    watch: {
    product(value) {
        this.currentIndex = 0

        document.body.style.overflow = value
        ? 'hidden'
        : ''
    }
    },

  mounted() {
    window.addEventListener('keydown', this.handleKeydown)
  },

  beforeDestroy() {
    window.removeEventListener('keydown', this.handleKeydown)
    document.body.style.overflow = ''
  },

  methods: {
    nextImage() {
        this.slideDirection = 'slide-next'

        if (this.currentIndex < this.product.images.length - 1) {
            this.currentIndex++
        } else {
            this.currentIndex = 0
        }
    },


    prevImage() {
        this.slideDirection = 'slide-prev'

        if (this.currentIndex > 0) {
            this.currentIndex--
        } else {
            this.currentIndex = this.product.images.length - 1
        }
    },

    formatPrice(value) {
      return value.toLocaleString('ru-RU')
    },

      handleKeydown(event) {
        if (event.key === 'Escape') {
            this.$emit('close')
        }
      }
  }
}
</script>


<style lang="scss">

.modal {
  position: fixed;
  inset: 0;

  z-index: 1000;

  display: flex;
  align-items: center;
  justify-content: center;

  padding: 20px;

  background: rgba(0,0,0,.45);


  &__window {
    position: relative;

    width: 760px;
    max-width: 100%;

    max-height: calc(100vh - 40px);

    overflow-y: auto;

    background: $background-color;
  }


  &__close {
    position: absolute;

    top: 12px;
    right: 16px;

    z-index: 5;

    width: 32px;
    height: 32px;

    border: none;

    background: transparent;

    color: $text-color;

    font-size: 28px;

    cursor: pointer;
  }


    &__slider {
    position: relative;

    width: 100%;

    overflow: hidden;
    }


    &__image {
    width: 100%;
    height: auto;

    display: block;

    object-fit: contain;

    background: #fff;

    position: relative;
    }


  &__controls {
    position: absolute;

    bottom: 20px;

    left: 0;
    right: 0;

    display: flex;
    justify-content: center;

    gap: 12px;
  }


  &__arrow {
    width: 36px;
    height: 36px;

    border: none;

    background: $accent-color;

    color: #fff;

    cursor: pointer;

    transition: background $transition;


    &:hover {
      background: $hover-color;
    }
  }


  &__content {
    padding: 32px;
  }


  &__title {
    margin: 0 0 24px;

    color: $text-color;

    font-size: 24px;

    font-weight: 700;

    line-height: 150%;
  }


  &__description {
    margin: 0 0 24px;

    color: $text-color;

    font-size: 14px;

    line-height: 150%;
  }


  &__price {
    color: $text-color;

    font-size: 18px;

    font-weight: 700;
  }


  &__sold {
    color: $text-color;

    font-size: 16px;

    font-weight: 700;
  }
}


/* открытие / закрытие */

.modal-enter-active,
.modal-leave-active {
  transition: opacity .3s ease;
}


.modal-enter-active .modal__window,
.modal-leave-active .modal__window {
  transition:
    transform .35s cubic-bezier(.22,1,.36,1),
    opacity .35s ease;
}


.modal-enter,
.modal-leave-to {
  opacity: 0;
}


.modal-enter .modal__window,
.modal-leave-to .modal__window {
  opacity: 0;
  transform: translateY(25px) scale(.97);
}


.modal-enter-to .modal__window {
  opacity: 1;
  transform: translateY(0) scale(1);
}


/* смена картинок */

.slide-next-enter-active,
.slide-next-leave-active,
.slide-prev-enter-active,
.slide-prev-leave-active {
  transition:
    transform .35s cubic-bezier(.22, 1, .36, 1),
    opacity .35s ease;
}


/* вперед → новая приходит справа */
.slide-next-enter {
  opacity: 0;
  transform: translateX(40px);
}

.slide-next-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-next-leave-to {
  opacity: 0;
  transform: translateX(-40px);
}


/* назад → новая приходит слева */
.slide-prev-enter {
  opacity: 0;
  transform: translateX(-40px);
}

.slide-prev-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-prev-leave-to {
  opacity: 0;
  transform: translateX(40px);
}

.modal__slider {
  display: grid;
}

.modal__image {
  grid-area: 1 / 1;
}


@media (max-width: 768px) {

  .modal {

    padding: 16px;


    &__content {
      padding: 24px;
    }


    &__title {
      font-size: 20px;
    }

  }

}

</style>