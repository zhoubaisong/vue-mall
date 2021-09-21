<template>
    <div class="goods">
      <GoodsItem class="item" v-for="item in goods" :goodsItem="item"/>
    </div>
</template>

<script>
    import GoodsItem from "./goodsItem";
    export default {
      name: "goods",
      props: {
        goods: {
          type: Array,
          default() {
            return [];
          }
        }
      },
      components: {GoodsItem}
    }
</script>

<style scoped>
  .goods{
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
    margin-top: 6px;
    padding: 0 4px;
  }
  .item{
    width: 50%;
  }

</style>
