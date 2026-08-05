<template>
  <footer class="footer">
    <div class="footer__container">

      <nav class="footer__nav">
        <a
          v-for="item in navigation"
          :key="item.id"
          :href="item.href"
          class="footer__link"
        >
          {{ item.title }}
        </a>
      </nav>

      <div class="footer__contacts">

        <a href="tel:+78125555555" class="footer__contact">
          <img
            :src="phoneIcon"
            alt="Телефон"
            class="footer__icon"
          />

          <span>
            +7 (812) 555-55-55
          </span>
        </a>

        <div class="footer__contact">
          <img
            :src="locationIcon"
            alt="Адрес"
            class="footer__icon"
          />

          <span>
            г. Санкт-Петербург, ул. Ефимова, 3
          </span>
        </div>

      </div>

    </div>
  </footer>
</template>

<script>
import navigation from '@/data/navigation'
import phoneIcon from '@/assets/icons/phone-icon.svg'
import locationIcon from '@/assets/icons/adress-icon.svg'

export default {
  name: 'AppFooter',

  data() {
    return {
      navigation,
      phoneIcon,
      locationIcon
    }
  }
}
</script>

<style lang="scss">
.footer {
  width: 100%;
  height: 95px;

  background: #ECEAEA;

  &__container {
    max-width: 1350px;
    margin: 0 auto;
    height: 100%;
    padding-left: 36px;
    padding-right: 20px;

    display: flex;
    align-items: center;
    gap: 0;
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
    letter-spacing: 0.7%;

    text-decoration: none;
    white-space: nowrap;

    transition: color $transition;

    &:hover {
      color: $hover-color;
      text-decoration: underline;
    }
  }

  &__contacts {
    display: flex;
    align-items: center;

    gap: 51px;
  }

  &__contact {
    display: flex;
    align-items: center;

    gap: 8px;

    color: $text-color;

    font-size: 14px;
    font-weight: 400;
    line-height: 150%;

    text-decoration: none;
    white-space: nowrap;
  }

  &__icon {
    width: 16px;
    height: 16px;

    flex-shrink: 0;
  }
}

@media (max-width: 1134px) {
  .footer {
    height: auto;

    &__container {
      flex-wrap: wrap;

      gap: 20px;

      padding: 20px;
    }

    &__nav {
      justify-content: left;
      gap: 24px;
    }

    &__contacts {
      gap: 24px;
    }
  }
}

@media (max-width: 840px) {
  .footer {
    &__container {
      flex-direction: column;
      align-items: flex-start;
    }
  }
}

@media (max-width: 485px) {
  .footer {
    &__nav {
      flex-direction: column;
      align-items: flex-start;

      gap: 10px;
    }

    &__contacts {
      flex-direction: column;
      align-items: flex-start;

      gap: 16px;
    }
  }
}

@media (max-width: 360px) {
  .footer {
    &__contact {
      font-size: 13px;
    }
  }
}
</style>