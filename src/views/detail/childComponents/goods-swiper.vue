<template>
  <Swiper class="detailSwiper">
    <SwiperItem v-for="(item, index) in topImages" :key="index">
      <img :src="item">
    </SwiperItem>
  </Swiper>
</template>

<script>
    import {Swiper, SwiperItem} from 'components/common/swiper/index';
    export default {
      name: "goods-swiper",
      props: {
        topImages: {
          type: Array,
          default() {
            return [];
          }
        }
      },
      components: {
        Swiper,
        SwiperItem
      },
      created() {
        console.log("swiper:", this.topImages)
      }
    }
</script>

<style scoped>
  .detailSwiper{
    height: 260px;
    overflow: hidden;
  }
</style>
