<template>
  <figure class="photo" @click="photoClick">
    <img :src="photo.fileName" :alt="photo.desc"/>
    <figcaption>
      <h2 class="img-title">{{photo.title}}</h2>
      <p class="img-back">{{photo.desc}}</p>
    </figcaption>
  </figure>
</template>

<script>
export default {
  props: ['photo', 'index'],
  methods: {
    photoClick(){
      this.$dispatch('photo-msg', this.index);
    }
  },
}
</script>

<style scoped>
  .photo{
    position: absolute;
    will-change: transform;
    width: 320px;
      height: 360px;
      margin: 0;
      padding: 40px;
      background-color: #fff;
      box-sizing: border-box;
      cursor: pointer;
      transform-style: preserve-3d;
      transition: transform .6s ease-in-out, left .6s ease-in-out, top .6s ease-in-out;
      box-shadow: 1px 2px 5px #666;
  }
  .photo img{
    opacity: 1;
    transition: opacity .6s ease-in-out;
  }
  figure.center{
    transform-origin: 0 50% 0;
  }
  figure.inverse img{
    opacity: 0;
    visibility: hidden;
  }
  figcaption{
    text-align: center;
  }
  .img-back{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    padding: 50px 40px;
    overflow: auto;
    color: #a7a0a2;
    font-size: 22px;
    line-height: 1.25;
    text-align: left;
    background-color: #fff;
    box-sizing: border-box;
    transform: rotateY(180deg) translateZ(1px);
    backface-visibility: hidden;
    text-align: center;
  }
  .img-title {
    margin: 20px 0 0 0;
    color: #a7a0a2;
    font-size: 16px;
  }
</style>
