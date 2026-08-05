<template>
  <header class="header">
    <div class="container header__container">

      <nav class="header__nav">
        <a
          v-for="item in navigation"
          :key="item.id"
          :href="item.href"
          class="header__link"
        >
          {{ item.title }}
        </a>
      </nav>

      <div class="header__search">
        <input
          class="header__input"
          type="text"
          :placeholder="searchPlaceholder"
        />

        <button class="header__button">
          Найти
        </button>
      </div>

    </div>
  </header>
</template>

<script>
import navigation from '@/data/navigation'

export default {
  name: 'AppHeader',

  data() {
    return {
      windowWidth: window.innerWidth,
      navigation
    }
  },

  computed: {
    searchPlaceholder() {
      return this.windowWidth >= 1024
        ? 'Поиск по названию картины'
        : 'Поиск'
    }
  },

  mounted() {
    window.addEventListener('resize', this.handleResize)
  },

  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize)
  },

  methods: {
    handleResize() {
      this.windowWidth = window.innerWidth
    }
  }
}
</script>

<style lang="scss">
.header {
  width: 100%;
  height: 95px;

  border-bottom: 1px solid $border-color;

  &__container {
    display: flex;
    align-items: center;
    gap: 67px;
    min-height: 100%;
    height: 100%;
    padding-bottom: 4px;
  }

  &__nav {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    gap: 48px;
  }

  &__link {
    color: $text-color;

    font-size: 14px;
    font-weight: 400;
    line-height: 150%;
    vertical-align: middle;
    letter-spacing: 0.7%;

    text-decoration: none;
    white-space: nowrap;

    transition: color $transition;

    &:hover {
      color: $hover-color;
      text-decoration: underline;
    }
  }

  &__search {
    display: flex;

    height: 48px;
  }

  &__input {
    width: 294px;

    padding: 0 16px;

    border: 1px solid $border-color;
    border-right: none;

    background: transparent;

    color: $text-color;

    font-family: inherit;
    font-size: 14px;
    font-weight: 400;
    line-height: 150%;
    vertical-align: middle;
    transition: all $transition;

    transition: border-color $transition;

    &::placeholder {
      color: #9F9F9F;
    }

    &:focus {
      outline: none;
      border-color: $accent-color;
    }
  }

  &__button {
    width: 122px;

    background: #403432;

    color: #fff;

    font-family: inherit;
    font-size: 14px;
    font-weight: 700;
    line-height: 150%;
    vertical-align: middle;

    cursor: pointer;

    transition: background $transition;

    &:hover {
      background: $hover-color;
    }

    &:active {
      background: $activate-color;
    }
  }
}

@media (max-width: 1024px) {
  .header {
    height: 76px;

    &__container {
      padding: 20px;
    }

    &__nav {
      gap: 24px;
    }

    &__search {
      height: 40px;
    }

    &__input {
      width: 220px;
    }
  }
}

@media (max-width: 840px) {
  .header {
    height: max-content;

    &__container {
      flex-wrap: wrap;
      align-items: stretch;

      gap: 20px;
    }

    &__nav {
      overflow-x: auto;

      gap: 24px;
    }

    &__search {
      width: 100%;
    }

    &__input {
      flex: 1;

      width: auto;
    }
  }
}

@media (max-width: 485px) {
  .header {
    &__container {
      gap: 16px;

      padding: 16px;
    }

    &__nav {
      flex-wrap: wrap;

      gap: 8px 16px;
    }
  }
}

@media (max-width: 360px) {
  .header {
    &__button {
      width: 100px;
    }
  }
}
</style>