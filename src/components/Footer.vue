<script>
export default {
  
}
</script>

<template>
  
  <footer class="footer">
    <div class="container">
      
      <div class="footer__social">
        <a href="https://github.com/Fayozxon" target="_blank">
          <img src="../assets/logo-github.svg" alt="Github logo">
          Github
        </a>
        <a href="https://dribbble.com/fayozxon" target="_blank">
          <img src="../assets/logo-dribbble.svg" alt="Dribbble logo">
          Dribbble
        </a>
        <a href="https://t.me/fayozhons" target="_blank">
          <img src="../assets/logo-telegram.svg" alt="Telegram logo">
          Telegram
        </a>
      </div>

      <p class="footer__text">2023 | @fayozhons tomonidan.</p>

    </div>
  </footer>

</template>

<style lang="scss" scoped>
@import '../main.scss';

.footer {
  margin-top: 156px;
  padding: 72px 0;
  background: $clr-primary-200;

  &__social {
    display: flex;
    flex-direction: column;
    gap: 16px;
    padding-bottom: 56px;

    a {
      display: flex;
      align-items: center;
      gap: 10px;
      color: $clr-primary-500;
    }
  }
}
</style>
