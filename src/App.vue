<template>
  <div id="app">
    <Nav />
    <Spinner color="hotpink"/>
    <div class="main-container">
      <h1>{{ cart }}</h1>
      <ImageGallery />
    </div>
  </div>
</template>

<script>
import ImageGallery from './components/ImageGallery.vue';
import Nav from './components/Nav.vue';
import Spinner from './components/Spinner.vue';

export default {
  name: 'app',
  components: {
    ImageGallery,
    Nav,
    Spinner
  }
}
</script>

<style lang="scss">

  body {
    margin:0px;
  }
  #app {
    margin-top: 60px;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    text-align: center;
  }

  .main-container{
    max-width:1120px;
    margin:auto;
    display: block ;
    margin-top:60px;
  }
</style>
