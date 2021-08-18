<template>
  <div class="slider">
    <div class="slider__container">
      <div class="slider__wrapper">
        <div
          class="slider__items"
          ref="slider-items"
          :style="{ transition: transition + 's' }"
        >
          <slot></slot>
        </div>
        <div
          v-if="hasPrevImage"
          class="slider__control slider__left"
          data-slide="prev"
        >
          <span @click="slideLeft">
            <i class="arrow arrow__left"></i>
          </span>
        </div>
        <div
          v-if="hasNextImage"
          class="slider__control slider__right"
          data-slide="next"
        >
          <span @click="slideRight">
            <i class="arrow arrow__right"></i>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: 'VueCarousel',
  props: {
    visibleCount: {
      type: Number,
      default() {
        return 1;
      },
    },
    transition: {
      type: Number,
      default() {
        return 0;
      },
    },
  },
  data() {
    return {
      currentPos: 0,
      currentImageIdx: 0,
      imagesCount: 0,
    };
  },
  mounted() {
    this.imagesCount = this.$refs['slider-items'].children.length;
  },
  methods: {
    getImgUrl(path) {
      return require(path);
    },
    slideLeft() {
      const $sliderItems = this.$refs['slider-items'];
      this.currentPos += $sliderItems.getBoundingClientRect().width;
      $sliderItems.style.transform = `translateX(${this.currentPos}px)`;
    },
    slideRight() {
      const $sliderItems = this.$refs['slider-items'];
      this.currentPos -= $sliderItems.getBoundingClientRect().width;
      $sliderItems.style.transform = `translateX(${this.currentPos}px)`;
    },
  },
  computed: {
    hasNextImage() {
      return this.imagesCount - 1 !== this.currentImageIdx;
    },
    hasPrevImage() {
      return this.currentImageIdx !== 0;
    },
  },
  watch: {
    currentPos(currentPos, prevPos) {
      if (currentPos < prevPos) {
        this.currentImageIdx += 1;
      } else {
        this.currentImageIdx -= 1;
      }
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}

.slider {
  position: relative;
}

.slider__items {
  margin: auto;
  width: 700px;
  display: flex;
}

.slider__wrapper {
  overflow: hidden;
}

.slider__control {
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: absolute;
  top: 0;
  bottom: 0;
  padding: 0 1em;
}

.slider__control > span {
  background-color: rgba(107, 107, 107, 0.575);
  padding: 11px;
  border-radius: 50%;
  cursor: pointer;
}

.slider__control > span:hover {
  opacity: 0.9;
}

.slider__left {
  left: 0;
}

.slider__right {
  right: 0;
}

i {
  border: solid white;
  border-width: 0 3px 3px 0;
  display: block;
  padding: 3px;
  width: 12px;
  height: 12px;
}

.arrow__left {
  transform: rotate(135deg);
}

.arrow__right {
  transform: rotate(-45deg);
}
</style>
