<template lang="pug">
#commodityList.flexBox
  ul.c1.leftList
    li.listBtn(v-for="item in searchLists" @click="searchItem(item.value)") {{item.name}}
  ul.c2.content.flexBox
    li.listBox(v-for="item in dataJSON" :class="{active: item.checked}" @click= "showDialog(item)") 
      input(type="checkbox" v-model="item.checked")
      img(:src="item.image")
      p {{item.name}}
  #dialog(v-show="dialogShow")
    .dialogBox
      img(:src="dialogVal.image")
      p {{dialogVal.name}}
      i.iconfont.iconclose(@click="dialogShow = false")
</template>
<script>
export default {
  props: ["dataJSON"],
  data() {
    return {
      searchLists: [
        { name: "New York", value: "New York" },
        { name: "London", value: "London" },
        { name: "Paris", value: "Paris" },
        { name: "Vancouver", value: "Vancouver" },
        { name: "Taiwan", value: "Taiwan" },
        { name: "Clean", value: "" }
      ],
      dialogShow: false,
      dialogVal: {}
    };
  },
  methods: {
    searchItem(val) {
      this.dataJSON.forEach(data => {
        if (data.name === val) {
          data.checked = true;
        } else {
          data.checked = false;
        }
      });
    },
    showDialog(item) {
      this.dialogShow = true
      this.dialogVal = item;
      console.log(this.dialogVal)
    }
  }
};
</script>
<style lang="sass">
#commodityList
  margin-top: 20px
  justify-content: space-between
  align-items: flex-start
  .leftList
    width: 12%
    .listBtn
      text-align: center
      border: 1px solid
      margin-bottom: 5px
  .content
    width: calc(88% - 20px)
    // justify-content: space-between
    flex-wrap: wrap
    .listBox
      width: calc(100%/6 - 5px)
      text-align: center
      padding: 15px 20px
      border: 1px solid
      margin-bottom: 3px
      &.active
        border: 2px solid #7171e0
      &:not(:nth-child(6n))
        margin-right: 6px
      img
        width: 100%
        height: 80px
      p
        font-size: .85rem
        margin-top: 5px
  #dialog
    position: fixed
    width: 100vw
    height: 100vh
    background-color: rgba(#555,.8)
    left: 0
    top: 0
    z-index: 15
    .dialogBox
      position: fixed
      width: 60vw
      height: 60vw
      left: 0
      right: 0
      top: 20vw
      margin: auto
      text-align: center
      p
        color: #fff
        font-weight: bold
        font-size: 2rem
        margin-bottom: 10px
      i
        color: #fff
        font-size: 1.5rem
        opacity: .9
</style>