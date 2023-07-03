<script>
import Hero from './components/Hero.vue';
import Footer from './components/Footer.vue';
import Playground from './components/Playground.vue';
import Screen from './components/Screen.vue';
import domtoimage from 'dom-to-image';

export default {
  components: {Hero, Screen, Playground, Footer},
  data() {
    return {
      messages: [],
      isLightTheme: true,
      screenBgSrc: '',
      isBgBlurred: false
    }
  },
  methods: {
    addMessage(msg) {
      this.messages.unshift(msg);
    },
    switchScreenTheme() {
      this.isLightTheme = !this.isLightTheme;
    },
    deleteLastMessage() {
      this.messages.shift();
    },
    newScreenBg(imgSrc) {
      this.screenBgSrc = imgSrc;
    },
    makeBgBlurred() {
      this.isBgBlurred = !this.isBgBlurred;
    },
    takeScreenshot() {
      domtoimage.toJpeg(document.getElementById('screen'), { quality: 1 })
        .then(function (dataUrl) {
            var link = document.createElement('a');
            link.download = 'telesim-screenshot.jpeg';
            link.href = dataUrl;
            link.click();
        });
    }
  }
}
</script>

<template>
  
  <main class="main">

    <Hero></Hero>

    <section class="main-section" id="main">
      
      <Screen
        :messages="messages"
        :isLightTheme="isLightTheme"
        :screenBgSrc="screenBgSrc"
        :isBgBlurred="isBgBlurred">
      </Screen>
      <Playground
        @addMessage="addMessage"
        :isLightTheme="isLightTheme"
        @switchScreenTheme="switchScreenTheme"
        @deleteLastMessage="deleteLastMessage"
        @newScreenBg="newScreenBg"
        @makeBgBlurred="makeBgBlurred"
        @takeScreenshot="takeScreenshot">
      </Playground>

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
    align-items: center;

    & > div {
      max-width: 400px;
      width: 100%;
    }
  }

  @media only screen and (max-width: 456px) {
    padding-left: 0;
    padding-right: 0;

    .playground {
      padding-left: 2rem;
      padding-right: 2rem;
      padding-top: 2rem;
    }
  }
}
</style>
