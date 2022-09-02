<template>
  <div class="app-container">
    <Header :app-name="appName" />

    <Main />

    <Footer />
  </div>
</template>

<script>
import Header from './Header';
import Main from './Main';
import Footer from './Footer';

const APP_NAME = 'Cryptocurrency Rate';

export default {
  name: 'App',

  components: {
    Header,
    Main,
    Footer,
  },

  data: () => ({
    appName: APP_NAME
  })
};
</script>

<style lang="scss">
.app-container {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>
