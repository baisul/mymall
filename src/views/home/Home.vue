<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物车</div>
    </nav-bar>
   <home-swiper :banners="banners"/>
    <recommend-view :recommends="recommends"/>
    <feature-view/>
    <tab-controll class="tab-controll" :titles="['流行','新款','精选']"
    @tabClick="tabClick"/>
    <goods-list :goods="showGoodsList"/>
    <ul>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
      <li>列表1</li>
      <li>列表2</li>
      <li>列表3</li>
      <li>列表4</li>
      <li>列表5</li>
      <li>列表6</li>
      <li>列表7</li>
      <li>列表8</li>
      <li>列表9</li>
      <li>列表10</li>
    </ul>
  </div>
</template>

<script>
  import HomeSwiper from "./childComponents/HomeSwiper";
  import RecommendView from "./childComponents/RecommendView";
  import FeatureView from "./childComponents/FeatureView";

  import NavBar from "components/common/navbar/NavBar";
  import TabControll from "components/content/tabControll/TabControll";
  import GoodsList from "../../components/content/goods/GoodsList";

  import {getHomeMultiData,getHomeGoods} from "network/home";
  export default {
        name: "Home",
    data() {
          return{
            banners: [],
            recommends: [],
            goods: {
              'pop': {page: 0,list: []},
              'new': {page: 0,list: []},
              'sell': {page: 0,list: []}
            },
            currentType: 'pop'
          }
    },
    computed: {
          showGoodsList() {
            return this.goods[this.currentType].list
          }
    },
      components: {
        GoodsList,
        NavBar,
        TabControll,
        HomeSwiper,
        RecommendView,
        FeatureView
        },
    created() {
      this.getHomeMultiData()
      //请求首页商品数据
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')
    },
    methods: {
    //事件监听的方法
     tabClick(index) {
        console.log(index)
       switch (index) {
          case 0:
               this.currentType = 'pop'
               break
         case 1:
              this.currentType = 'new'
               break
         case 2:
              this.currentType = 'sell'
               break
       }
     },
      //网路请求的方法
      getHomeMultiData() {
            getHomeMultiData().then(res => {
              this.banners = res.data.banner.list
              this.recommends = res.data.recommend.list
            })
          },
      getHomeGoods(type) {
            const page = this.goods[type].page + 1
        getHomeGoods(type,page).then(res => {
          console.log(this.goods[type].list)
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page += 1
        })
      }
    }
  }
</script>

<style scoped>
  #home{
    padding-top: 44px;
  }
  .home-nav{
    background-color: #ff8198;
    color: #fff;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 9;
  }
  .tab-controll{
    position: sticky;
    top: 44px;
    z-index: 9;
  }
</style>
