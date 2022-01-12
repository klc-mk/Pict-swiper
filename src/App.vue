<template>
  <div id="app">
  <p>
    <PictSwiper srcA='images/sample_pict_A.jpg' srcB='images/sample_pict_B.jpg'/>
  </p>

  </div>
</template>

<script>
import PictSwiper from './components/pict-swiper.vue'

export default {
  name: 'App',
  components: {
    PictSwiper
  }
}
</script>

<style>

</style>
