<script>
import Hero from './components/Hero.vue';
import Footer from './components/Footer.vue';
import Playground from './components/Playground.vue';
import Screen from './components/Screen.vue';

export default {
  components: {Hero, Screen, Playground, Footer}
}
</script>

<template>
  
  <main class="main">

    <Hero></Hero>

    <section class="main-section" id="main">
      
      <Screen></Screen>
      <Playground></Playground>

    </section>

    <Footer></Footer>

  </main>

</template>

<style lang="scss" scoped>
@import './main.scss';

.main-section {
  max-width: 814px;
  margin: 0 auto;
  padding: 0 2rem;
  display: flex;
  gap: 20px;
  padding-top: 156px;

  & > div {
    width: 50%;
  }

  @media only screen and (max-width: 825px) {
    flex-direction: column;

    & > div {
      width: 100%;
    }
  }
}
</style>
