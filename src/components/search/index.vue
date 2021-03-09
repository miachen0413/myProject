<template lang="pug">
#search
  //- p {{dataJSON}}
  .searchBox.flexBox
    i.iconfont.iconsearch
    .inputBox
      input(type="text" placeholder="Search" v-model="searchData")
    i.iconfont.iconclose
</template>
<script>
export default {
  props: ["dataJSON"],
  data() {
    return {
      searchData: "",
      timer: null
    };
  },
  watch: {
    searchData(val) {
      clearTimeout(this.timer);
      this.timer = setTimeout(() => {
        var searchData = this.dataJSON.filter(
          data => data.name.indexOf(val) != -1
        );
        this.$emit("search", searchData);
      }, 300);
    }
  }
};
</script>
<style lang="sass" scoped>
#search
  padding: 10px 15px
  background: #ccc
  position: sticky
  z-index: 10
  top: 0
  .searchBox
    padding: 8px 15px
    background-color: #fff
    border-radius: 2px
    i
      font-size: 1.3rem
    .inputBox
      width: 100%
      margin-left: 15px
      input
        width: 100%
        border: none
        font-size: 1.1rem
        outline: none
        
</style>