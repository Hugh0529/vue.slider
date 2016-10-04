<template>
  <div class="col-md-3 col-md-offset-4">
    <slider :pics="sliderOption.pics" :height="sliderOption.height" :is-show-number="sliderOption.isShowNumber"></slider>
  </div>
</template>

<script>
  import Slider from '../../slider/Slider.vue'

  export default {
    components: {
      Slider: Slider
    },

    data: function () {
      return {
        sliderOption: {
          height: 325,
          isShowNumber: true,
          speed: 1,
          pics: [
            'http://img2.ooopic.com/13/98/46/32bOOOPICb2_202.jpg',
            'http://img2.ooopic.com/13/06/20/82bOOOPIC87_202.jpg',
            'http://img2.ooopic.com/13/66/08/73bOOOPIC12_202.jpg'
          ]
        }
      }
    }
  }
</script>

<style>

</style>
