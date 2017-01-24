<template>
  <div id="app">
    <div class="stage">
      <photo-component v-for="(index, photo) in photoes" track-by="$index" @photo-msg="handleChange" :index="index" :photo="photo" :style="styObj[index]"></photo-component>
    </div>
    <div class="contrls">
      <ctrl-component v-for="index in photoes.length" :index="index" :active="active" @ctrl-msg="handleChange"></ctrl-component>
    </div>
  </div>
</template>

<script>
import Photo from './components/Photo';
import Ctrl from './components/Ctrl';

export default {
  components: {
    'photo-component': Photo,
    'ctrl-component': Ctrl,
  },
  data: function(){
    return {
      photoes: [
        {
          "fileName": require('./assets/images/1.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer."
        },
        {
          "fileName": require('./assets/images/2.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer."
        },
        {
          "fileName": require('./assets/images/3.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer."
        },
        {
          "fileName": require('./assets/images/4.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/5.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/6.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/7.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/8.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/9.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/10.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/11.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer. "
        },
        {
          "fileName": require('./assets/images/12.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer.  "
        },
        {
          "fileName": require('./assets/images/13.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer.  "
        },
        {
          "fileName": require('./assets/images/14.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer.  "
        },
        {
          "fileName": require('./assets/images/15.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer.  "
        },
        {
          "fileName": require('./assets/images/16.jpg'),
          "title": "Heaven of time",
          "desc": "Here he comes Here comes Speed Racer.  "
        }
      ],
      active: '',
      styObj: [],
      leftSec: {},
      rightSec: {},
      topSec: {},
      center: {},
      photoDOM: [],
      ctrlDOM: [],
    };
  },
  ready (){
    this.active = Math.trunc(Math.random() * this.photoes.length);
    this.photoDOM = document.querySelectorAll('.photo');
    this.ctrlDOM = document.querySelectorAll('.contrls span');

    const stage = document.querySelector('.stage');
    let imgFigure = document.querySelector('.photo');
    var  {scrollWidth, scrollHeight} = stage;
    const stageWidth = scrollWidth;
    const stageHeight = scrollHeight;
    const stageHalfWidth = Math.ceil(stageWidth / 2);
    const stageHalfHeight = Math.ceil(stageHeight / 2);
    var {scrollWidth, scrollHeight} = imgFigure;
    const imgFigureWidth = scrollWidth;
    const imgFigureHeight = scrollHeight;
    const imgFigureHalfWidth = Math.ceil(imgFigureWidth / 2);
    const imgFigureHalfHeight = Math.ceil(imgFigureHeight / 2);

    this.leftSec = {
      hPosRange: [-imgFigureHalfWidth, stageHalfWidth - imgFigureHalfWidth * 3],
      vPosRange: [-imgFigureHalfHeight, stageHeight - imgFigureHalfHeight],
    },
    this.rightSec = {
      hPosRange: [stageHalfWidth + imgFigureHalfWidth, stageWidth - imgFigureHalfWidth],
      vPosRange: [-imgFigureHalfHeight, stageHeight - imgFigureHalfHeight],
    }
    this.topSec = {
      hPosRange: [stageHalfWidth - imgFigureWidth, stageHalfWidth],
      vPosRange: [-imgFigureHeight, stageHalfHeight - imgFigureHalfHeight * 3],
    }
    this.center = {
      left: stageHalfWidth - imgFigureHalfWidth,
      top: stageHalfHeight - imgFigureHalfHeight,
    }

    this.styObj = this.addStyObj();
  },
  methods: {
    handleChange (index){
      this.photoDOM[index].classList.add('center');
      if(index === this.active){
        this.ctrlDOM[index].classList.toggle('inverse');
        this.photoDOM[index].classList.toggle('inverse');
        const inverse = document.querySelector('.inverse');
        this.styObj[index].transform = !inverse ? `translate(${this.center.left}px, ${this.center.top}px)` : `translate(${this.center.left + 320}px, ${this.center.top}px) rotateY(180deg)`;
        this.styObj.$set(index, this.styObj[index]);
      }else{
        const inverse = document.querySelectorAll('.inverse');
        inverse.length && Array.from(inverse).forEach((elem)=>{
          elem.classList.remove('inverse');
        })
        this.active = index;
        this.styObj = this.addStyObj();
      }
    },
    addStyObj (){
      let arr = [];
      const k = this.photoes.length / 2;
      let isTop = false;
      for(let i = 0 ; i < this.photoes.length ; i++){
        if(this.active !== i){
          if(!isTop && Math.random() > 0.5){
            var left = this.getRandom(this.topSec.hPosRange[0], this.topSec.hPosRange[1]);
            var top = this.getRandom(this.topSec.vPosRange[0], this.topSec.vPosRange[1]);
            arr.push({
              transform: `translate(${left}px, ${top}px) rotate(${30 * (2 * Math.random() - 1)}deg`,
              zIndex: '9',
            });
            isTop = true;
            continue;
          }
          if(i < k){
            var left = this.getRandom(this.leftSec.hPosRange[0], this.leftSec.hPosRange[1]);
            var top = this.getRandom(this.leftSec.vPosRange[0], this.leftSec.vPosRange[1]);
          }else{
            var left = this.getRandom(this.rightSec.hPosRange[0], this.rightSec.hPosRange[1]);
            var top = this.getRandom(this.rightSec.vPosRange[0], this.rightSec.vPosRange[1]);
          }
          arr.push({
            transform: `translate(${left}px, ${top}px) rotate(${30 * (2 * Math.random() - 1)}deg`,
            zIndex: '9',
          })
        }else{
          arr.push({
            transform: `translate(${this.center.left}px, ${this.center.top}px)`,
            zIndex: '99',
          })
        }
      }
      return arr;
    },
    getRandom (low, high){
      return Math.floor(Math.random() * (high - low) + low);
    }
  },
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}
@font-face {
  font-family: "icons-turn-arrow";
  src: url("./assets/fonts/icons/turn-arrow.eot") format("embedded-opentype"), url("./assets/fonts/icons/turn-arrow.woff") format("woff"), url("./assets/fonts/icons/turn-arrow.ttf") format("truetype"), url("./assets/fonts/icons/turn-arrow.svg") format("svg");
}
body{
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: #ddd;
  perspective: 1800px;
}
.stage {
  position: relative;
  width: 100%;
  height: 680px;
}
.contrls{
  position: absolute;
  left: 0;
  bottom: 30px;
  z-index: 101;
  width: 100%;
  text-align: center;
}
</style>
