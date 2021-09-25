<template>
  <div id="detail">
    <GoodsNavBar class="navBar"></GoodsNavBar>
    <Bscroll class="content" ref="scroll">
      <GoodsSwiper :top-images="topImages" @swiperImageLoad="imageLoaded"></GoodsSwiper>
      <GoodsBaseInfo :goods="goods"></GoodsBaseInfo>
      <GoodsShopInfo :shop="shop"></GoodsShopInfo>
      <GoodsGoodsInfo :detailInfo="detailInfo"></GoodsGoodsInfo>
      <goods-param-info :param-info="paramInfo"></goods-param-info>
      <GoodsRecommend :goods="recommend" @getGoodsDetail="goodsDetail(iid)"></GoodsRecommend>
    </Bscroll>
  </div>
</template>

<script>
    import GoodsNavBar from "./childComponents/goods-navbar"
    import GoodsSwiper from './childComponents/goods-swiper'
    import GoodsBaseInfo from './childComponents/goods-base-info'
    import GoodsShopInfo from './childComponents/goods-shop-info'
    import GoodsGoodsInfo from './childComponents/goods-goods-info'
    import GoodsParamInfo from './childComponents/goods-param-info'
    import GoodsRecommend from 'components/content/goods/goods'

    import Bscroll from "components/common/bscroll/bscroll"
    import {getGoodsDetail, Goods, Shop, GoodsParam, recommend} from 'network/detail'

    export default {
      name: "goodsDetail",
      components: {
        GoodsNavBar,
        GoodsSwiper,
        GoodsBaseInfo,
        GoodsShopInfo,
        GoodsGoodsInfo,
        GoodsParamInfo,
        GoodsRecommend,
        Bscroll
      },
      data() {
        return {
          topImages: [],
          goods: {},
          shop: {},
          detailInfo: {},
          paramInfo: {},
          recommend: recommend
        }
      },
      created() {
        this.goodsDetail(this.$route.params.iid);
      },
      beforeRouteUpdate(to, from, next) {
        this.goodsDetail(to.params.iid);
      },
      updated() {
        this.$refs.scroll.scrollTop(0, 0, 0);
        this.$refs.scroll.refresh();
      },
      methods: {
        goodsDetail(iid) {
          getGoodsDetail(iid).then(res => {
            const result = res.result;
            this.topImages = result.itemInfo.topImages;//轮播图
            this.goods = new Goods(result.itemInfo, result.columns, result.shopInfo.services);
            this.shop = new Shop(result.shopInfo);
            this.detailInfo = result.detailInfo;
            // 5.获取参数的信息
            this.paramInfo = new GoodsParam(result.itemParams.info, result.itemParams.rule);
          })
        },
        imageLoaded() {
          this.$refs.scroll.refresh();
        }
      }
    }
</script>

<style scoped>
  #detail {
    position: relative;
    z-index: 999;
    background-color: #fff;
    height: 100vh;
  }
  .content {
    height: calc(100% - 44px);
    background-color: #fff;
    z-index: 999;
    margin-top: 44px;
  }
  .navBar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    background-color: #fff;
    z-index: 9;
  }
</style>
