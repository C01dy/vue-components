<template>
  <div style="display: flex; justify-content: center;">
    <vue-carousel :transition="0.3">
      <vue-carousel-item
        v-for="(item, idx) in images"
        :key="idx"
        :src="item.url"
      ></vue-carousel-item>
    </vue-carousel>
  </div>
</template>

<script>
import VueCarousel from './components/VueCarousel';
import VueCarouselItem from './components/VueCarousel/VueCarouselItem';

export default {
  name: 'App',
  data() {
    return {
      images: [
        {
          title: 'title 1',
          url:
            'https://images.wallpaperscraft.ru/image/devushki_neko_ushki_218629_1280x720.jpg',
        },
        {
          title: 'title 2',
          url:
            'https://images.wallpaperscraft.ru/image/gorod_zdaniia_ogni_218626_1280x720.jpg',
        },
        {
          title: 'title 3',
          url:
            'https://images.wallpaperscraft.ru/image/soldat_voennyj_vintovka_218619_1280x720.jpg',
        },
        {
          title: 'title 4',
          url:
            'https://images.wallpaperscraft.ru/image/gepard_detenysh_zhivotnoe_218597_1280x720.jpg',
        },
      ],
    };
  },
  components: {
    VueCarousel,
    VueCarouselItem,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
