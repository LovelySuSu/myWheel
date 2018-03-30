<template>
  <div id="app">
    <slide-show :slideList="slides" :speed="speed"></slide-show>
  </div>
</template>

<script>

import SlideShow from './components/SlideShow.vue'
export default {
  name: 'App',
  data(){
    return {
      speed:2000,
      slides: [
        {
          src: require('../src/assets/p1.jpg')
        },
        {
          src: require('../src/assets/p2.jpg')
        },
        {
          src: require('../src/assets/p3.jpg')
        },
        {
          src: require('../src/assets/p4.jpg')
        }
      ],
    }
  },
  components: {
    SlideShow
  }
}
</script>

<style>


</style>
