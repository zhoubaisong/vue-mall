<template>
  <div>
    <GoodsNavBar></GoodsNavBar>
    <GoodsSwiper :top-images="topImages"></GoodsSwiper>
  </div>
</template>

<script>
    import GoodsNavBar from "./childComponents/goods-navbar"
    import GoodsSwiper from './childComponents/goods-swiper'
    import {getGoodsDetail} from 'network/detail';

    export default {
      name: "goodsDetail",
      components: {
        GoodsNavBar,
        GoodsSwiper
      },
      data() {
        return {
          iid: null,
          topImages: [],
          swiper: null
        }
      },
      beforeCreate() {
        this.iid = this.$route.params.iid;
        getGoodsDetail(this.iid).then(res => {
          this.topImages = res.result.itemInfo.topImages;//轮播图
        })
      }
    }
</script>

<style scoped>
</style>
