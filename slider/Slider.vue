<template>
  <div id="slider" class="product-images slick-initialized slick-slider" :style="getContainerStyle()">
    <div class="number-container" v-if="isShowNumber">{{current + 1}}/{{pics.length}}</div>
    <button type="button" class="slick-prev slick-arrow"
            data-role="none" aria-label="Previous" role="button" style="display: block;"
            @click="goPrev()">Previous</button>

    <div aria-live="polite" class="slick-list draggable">
      <div class="slick-track list-box" role="listbox" :style="getListBoxStyle()">
        <div class="slick-slide" data-slick-index="0"
             :style="getSlideBoxStyle(pic)"
             v-for="pic in pics">
        </div>
      </div>
    </div>

    <button type="button" class="slick-next slick-arrow"
            data-role="none" aria-label="Next" role="button" style="display: block;"
            @click="goNext()">Next</button>
  </div>
</template>

<script>
  export default {
    el: function () {
      return '#slider'
    },

    data: function () {
      return {
        translateX: 0,

        current: 0,

        defaultOption: {
          height: 300,
          speed: 1
        }
      }
    },

    props: {
      pics: {
        type: Array,
        required: true
      },

      isShowNumber: {
        type: Boolean,
        required: false
      },

      height: {
        type: Number,
        required: false
      },

      speed: {
        type: Number,
        required: false
      }

    },

    watch: {
      'current': function (newValue, oldValue) {
        this.translateX = this.translateX + 100 * (oldValue - newValue) / this.pics.length
      }
    },

    methods: {
      canGoPrev: function () {
        return this.current > 0
      },

      canGoNext: function () {
        return this.current < this.pics.length - 1
      },

      goPrev: function () {
        if (this.canGoPrev()) {
          this.current = this.current - 1
        }
      },

      goNext: function () {
        if (this.canGoNext()) {
          this.current = this.current + 1
        }
      },

      getListBoxStyle: function () {
        return {
          opacity: 1,
          width: this.pics.length * 100 + '%',
          height: '100%',
          transform: `translateX(${this.translateX}%)`,
          transition: `transform ${this.speed || this.defaultOption.speed}s`
        }
      },

      getSlideBoxStyle: function (pic) {
        return {
          width: 1 / (this.pics.length) * 100 + '%',
          height: (this.height || this.defaultOption.height) + 'px',
          background: `url(${pic}) center center no-repeat`,
          'background-size': 'contain'
        }
      },

      getContainerStyle: function () {
        return {
          height: (this.height || this.defaultOption.height) + 'px'
        }
      }
    }

  }

</script>

<style scoped>
  .slick-slider {
    position: relative;
    display: block;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }

  .slick-prev, .slick-next {
    font-size: 0;
    line-height: 0;
    position: absolute;
    top: 50%;
    display: block;
    width: 20px;
    height: 20px;
    margin-top: -10px;
    padding: 0;
    cursor: pointer;
    color: transparent;
    border: none;
    outline: none;
    background: transparent;
  }

  .slick-prev {
    left: -25px;
  }

  .slick-next {
    right: -25px;
  }

  .slick-slider .slick-track, .slick-slider .slick-list {
    -webkit-transform: translate3d(0, 0, 0);
    -moz-transform: translate3d(0, 0, 0);
    -ms-transform: translate3d(0, 0, 0);
    -o-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
  }

  .slick-list {
    position: relative;
    display: block;
    overflow: hidden;
    margin: 0;
    padding: 0;
    width: 100%;
  }

  .slick-track {
    position: relative;
    top: 0;
    left: 0;
    display: block;
  }

  .slick-slide {
    display: block;
    float: left;
    height: 100%;
    min-height: 1px;
  }

  .slick-prev:before, .slick-next:before {
    color: #1ab394 !important;
  }

  .slick-prev::before {
    content: "<";
  }

  .slick-next::before {
    content: ">";
  }

  .slick-prev:before, .slick-next:before {
    font-size: 20px;
    line-height: 1;
    opacity: .75;
    color: white;
  }

  .slick-track:after {
    clear: both;
  }

  .slick-track:before, .slick-track:after {
    display: table;
    content: '';
  }

  .number-container {
    text-align: center;
  }

</style>
