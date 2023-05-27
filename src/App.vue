<template>
  <div id="app">
    <art-header></art-header>
  </div>
</template>

<script>
import ArtHeader from './views/Art-header.vue'

export default {
  name: 'App',
  components: {
    ArtHeader
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter&family=Lato:wght@400;700&family=Montserrat:wght@500;600&family=Roboto&display=swap');
  #app {
    font-family: 'Montserrat';
    padding: 32px 65px 100px;
  }
</style>
