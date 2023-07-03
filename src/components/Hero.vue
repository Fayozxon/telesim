<script>
export default {
  
}
</script>

<template>
  
  <div class="container">

    <div class="hero-image">
      <img src="../assets/hero-image.png" alt="Telegram logo">
      <a href="https://github.com/Fayozxon/telesim" class="hero-image__star" target="_blank">
        <img src="../assets/icons/icon-star.gif" alt="Star icon">
        Githubda yulduz bosing
      </a>
    </div>
    
    <header class="header">
      <a href="/">
        <img src="../assets/logo.svg" alt="telesim logo" title="telesim logo" class="header__brand">
      </a>
    </header>

    <div class="language-switch" style="display: none;">
      <span>English</span>&nbsp&nbsp•&nbsp&nbsp<span class="active">O‘zbek</span>
    </div>

    <section class="hero-section">
      <h1 class="hero-section__title">Soxta Xabarlashish</h1>
      <p class="hero-section__text">
        Bu chat <a href="https://telegram.org/" target="_blank">Telegram</a>ning simulyatori. Brauzerni o'zida soxta xabarlarni hosil qiling va skrinshotlarni bepul yuklab olib do'stlaringizga yuboring! Faqatgina hazil sifatida ishlatishni maslahat beraman.
      </p>
      <a href="#main" class="btn">Sinab ko‘ring</a>
      <a href="https://github.com/Fayozxon/" class="btn btn-secondary">Muallif</a>
    </section>

  </div>

</template>

<style lang="scss" scoped>
@import '../main.scss';

.container {
  position: relative;
}

.hero-image {
  position: absolute;
  top: 0;
  right: 0;

  &:hover &__star {
    opacity: 1;
  }

  @media only screen and (max-width: 456px) {
    display: none;
  }

  &__star {
    position: absolute;
    display: flex;
    gap: 10px;
    align-items: center;
    top: 50%;
    transform: translateY(-60%);
    left: 20px;
    right: 20px;
    background: $clr-opaque;
    padding: 10px 20px;
    backdrop-filter: blur(12px);
    box-shadow: 0px 5px 20px 0px rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    color: $clr-primary-500;
    transition: $ts-200;
    opacity: 0;

    img {
      width: 24px;
    }
  }
}

.header {
  padding-top: 56px;
  padding-bottom: 40px;

  &__brand {
    width: 168px;
  }
}

.language-switch {
  font-size: $fs-100;
  cursor: default;

  span {
    cursor: pointer;

    &.active {
      color: $clr-accent-500;
    }
  }
}

.hero-section {
  padding-top: 60px;

  &__title {
    font-size: $fs-400;
    font-weight: 700;
  }

  &__text {
    padding-top: 16px;
    padding-bottom: 32px;
    line-height: 1.9;
    color: $clr-primary-400;
  }

  .btn-secondary {
    margin-left: 24px;
  }
}
</style>
