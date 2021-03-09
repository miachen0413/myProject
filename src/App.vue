<template lang="pug">
#app
  .innerWidth
    search.r1(:dataJSON="dataJSON" @search="searchData")
    advertising.r2
    countdown.r3
    commodityList.r4(:dataJSON="searchJSON")
  button(type="submit" @click="goup").goup GOUp
</template>
<script>
import search from "./components/search/index.vue";
import advertising from "./components/advertising/index.vue";
import countdown from "./components/countdown/index.vue";
import commodityList from "./components/commodityList/index.vue";
import goUp from "./components/goUp/index.vue";
import dataJSON from "./index.json";
const components = {
  search,
  advertising,
  countdown,
  commodityList,
  goUp
};
export default {
  name: "app",
  components,
  data() {
    return {
      dataJSON,
      searchJSON: []
    };
  },
  methods: {
    searchData(val) {
      this.searchJSON = val;
    },
    goup() {
      // document.body.scrollTop = 0;
      // document.documentElement.scrollTop = 0;
      window.scrollTo(0,0)
    }
  },
  mounted() {
    this.searchJSON = JSON.parse(JSON.stringify(this.dataJSON));
  }
};
</script>
<style lang="sass">
@import './assets/style'
@import './assets/font/iconfont.css'
#app
  .goup
    position: fixed
    right: 30px
    bottom: 60px
    padding: 10px 15px
    background-color: #d5e4f9
    border: 1px solid #8686e4
    color: #657fff
</style>
