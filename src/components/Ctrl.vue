<template>
  <span :class="{active: this.index === this.active}" @click="ctrlClick(index)"></span>
</template>

<script>
export default {
  props: ['index', 'active'],
  methods: {
    ctrlClick(){
      this.$dispatch('ctrl-msg', this.index);
    }
  },
}
</script>

<style scoped>
  span{
    display: inline-block;
    will-change: transform;
      margin: 0 5px;
      width: 30px;
      height: 30px;
      text-align: center;
      vertical-align: middle;
      cursor: pointer;
      background-color: #aaa;
      border-radius: 50%;
      transform: scale(.5);
      transition: transform .6s ease-in-out, background-color .3s;
  }
  span.active{
    background-color: #888;
      transform: scale(1);
  }
  span.active:after{
    color: #fff;
      font-family: "icons-turn-arrow";
      font-size: 80%;
      line-height: 30px;
      content: "\e600";
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
  }
  span.inverse{
    background-color: #555;
      transform: rotateY(180deg);
  }
</style>
