<template>
  <div class="slider__item">
    <img :src="src" alt="image" />
  </div>
</template>

<script>
export default {
  name: 'VueCarouselItem',
  props: {
    src: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
.slider__item {
  flex: 0 0 100%;
}

.slider__item img {
  min-height: 100%;
  max-height: 100%;
}
</style>
