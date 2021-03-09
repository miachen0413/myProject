<template lang="pug">
#countdown
  .timer
    p 倒數 : {{day}} : {{hour}} : {{minute}} : {{second}}
</template>
<script>
export default {
  data() {
    return {
      // 一天毫秒
      millisecond: 1000 * 60 * 60 * 24,
      timer: null
    };
  },
  computed: {
    day() {
      return parseInt(this.millisecond / 24 / 60 / 60 / 1000);
    },
    hour() {
      return parseInt(this.millisecond / 60 / 60 / 1000 - this.day * 24);
    },
    minute() {
      return parseInt(
        this.millisecond / 60 / 1000 - this.day * 24 * 60 - this.hour * 60
      );
    },
    second() {
      return parseInt(
        this.millisecond / 1000 -
          this.day * 24 * 60 * 60 -
          this.hour * 60 * 60 -
          this.minute
           * 60
      );
    }
  },
  methods: {
    countDown() {
      this.timer = setInterval(() => {
        if (this.millisecond > 0) {
          this.millisecond = this.millisecond - 1000;
        } else {
          clearInterval(this.timer);
        }
      }, 1000);
    }
  },
  mounted() {
    this.countDown();
  }
};
</script>
<style lang="sass" scoped>
  #countdown
    border: 1px solid
    margin-top: 10px
</style>