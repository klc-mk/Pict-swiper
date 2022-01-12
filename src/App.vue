<template>
  <div id="app">
  <p>
    250px*250px
    <PictSwiper srcA='images/sample_pict_A.jpg' srcB='images/sample_pict_B.jpg'/>
  </p>
  
  <p>
    750px*750px
    <PictSwiper srcA='images/sample_pict_750A.jpg' srcB='images/sample_pict_750B.jpg'/>
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
