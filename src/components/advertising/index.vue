<template lang="pug">
#advertising
  .innerAdvertising.flexBox(:style="'left:-'+nowImgPosition*80+'vw'")
    .imgBox(v-for="img in imgs")
      img(:src="img")
  .left(@click="toImage(-1)")
    i.iconfont.iconback
  .right(@click="toImage(1)")
    i.iconfont.iconright
  .docBox.flexBox(:style="'width:'+imgLength*20+'px'")
    .doc(v-for="(docNum,idx) in imgLength" @click="goImage(idx)" :class="{active: idx === nowImgPosition}")
</template>
<script>
import img1 from "./image/001.jpg";
import img2 from "./image/002.jpg";
import img3 from "./image/003.jpg";
export default {
  data() {
    return {
      imgs: {
        img1: img1,
        img2: img2,
        img3: img3,
        img4: img1,
        img5: img2,
        img6: img3,
        img7: img1,
        img8: img2,
        img9: img2,
        img10: img3
      },
      nowImgPosition: 0,
      timer: null
    };
  },
  computed: {
    imgLength() {
      return Object.keys(this.imgs).length;
    }
  },
  methods: {
    goImage(idx) {
      if (this.nowImgPosition > 0 && this.nowImgPosition < this.imgLength) {
        this.nowImgPosition = idx;
      }
    },
    toImage(toIdx) {
      this.nowImgPosition += toIdx;
    },
    setTimeSlider() {
      this.timer = setInterval(() => {
        this.nowImgPosition =
          this.nowImgPosition < this.imgLength - 1
            ? this.nowImgPosition + 1
            : 0;
      }, 3000);
    }
  },
  mounted() {
    this.setTimeSlider();
  }
};
</script>
<style lang="sass">
#advertising
  width: 80vw
  height: 400px
  overflow: hidden
  position: relative
  .innerAdvertising
    width: calc(80vw * 3)
    position: absolute
    transition: .3s
    .imgBox
      img
        width: 80vw
        height: 400px
  .left,.right
    position: absolute
    transform: translateY(calc((400px - 1.5rem) / 2))
    color: #fff
    opacity: .8
    i
      font-size: 1.5rem
    &:active
      opacity: 1
  .right
    right: 10px
  .left
    left: 10px
  .docBox
    position: absolute
    left: 0
    right: 0
    bottom: 30px
    margin: auto
    .doc
      width: 8px
      height: 8px
      border-radius: 50%
      background-color: #fff
      margin: 0 5px
      opacity: .6
      &.active
        opacity: 1
      
</style>