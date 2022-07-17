<template>
  <div class="wrapper">
    <div class="head">
      <p>Актуальное</p>
      
      
      <div class="progress-indicator-wrapper">
        <div class="progress-indicator" :style="{ width: progress }"></div>
      </div>

      <div class="buttons">
        <button class="left" @click="left"></button>
        <button class="right" @click="right"></button>
      </div>
        
      
    </div>

    <div class="v-carousel"
    v-touch:swipe.left = "right"
    v-touch:swipe.right = "left"
    :style="{ 'margin-left': '-' + (100 * slideIndex) + '%' }">

      <v-carousel-item
        v-for="item in slideItems"
        :key="item.id"
        :item_data="item"
      />

    </div>

  </div>
</template>

<script>
import vCarouselItem from './v-carousel-item.vue'

export default {
  name: 'v-carousel',
  components: {
    vCarouselItem
  },
  props: {
    slideItems: {
      type: Array,
      default: () => []
    },
    interval: {
      type: Number,
      default: 0
    }
  },
  data(){
    return{
      slideIndex: 0,
      width: window.innerWidth,
      slideCycle: this.slideCycl(),
      visibleSlides: this.numberVisible(window.innerWidth),
      progress: "0%"
    }
  },
  methods:{
    left(){
      if(this.slideIndex > 0){
        this.slideIndex--
      }
    },
    right(){
      if(this.slideIndex === this.slideCycle ){
        this.slideIndex = 0
      }else{
        this.slideIndex++
      }
      this.updateProgressIndicator()
    },
    updateProgressIndicator() {
      this.progress = (100/this.slideCycle * this.slideIndex) + "%";
    },
    swipe(direction) {
      direction.target.style.position = 'absolute'
      direction.target.style.left = direction.changedTouches[0].clientX + 'px'
    },
    onResize() {
      this.width = window.innerWidth
      this.visibleSlides = this.numberVisible(window.innerWidth);
      this.slideCycle = this.slideCycl()
    },
    slideCycl(){
      return Math.ceil((this.slideItems.length/this.visibleSlides)-1)
    },
    numberVisible(width){
      if(width > 1110){
        return 4
      }
      if(width <= 1110 && width > 820){
        return 3
      }
      if(width <= 820 && width > 524){
        return 2
      }
      if(width <= 524){
        return 1
      }
      return 4
    }
  },
  mounted(){
    if (this.interval > 0) {
      let vm = this; 
      setInterval ( function() {
        vm.right()
      }, vm.interval)
    }
    this.$nextTick(() => {
      window.addEventListener('resize', this.onResize);
    })

    this.slideCycle = this.slideCycl()
  },
  beforeDestroy() { 
    window.removeEventListener('resize', this.onResize); 
  }
}
</script>

<style lang="scss">
.head{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.head p{
  font-family: 'Roboto';
  font-style: normal;
  font-weight: 700;
  font-size: 50px;
  line-height: 60px;
  color: #527CCD;
}

.buttons{
  display: flex;
}

//Progress Indicator
$header-height: 60px;
$progress-indicator-height: 5px;
$vue-green: #527CCD;
.progress-indicator-wrapper{
  margin-left: 20%;
  height: $progress-indicator-height;
  background-color: #C8D9FB;
  width: 100%;
  top: $header-height;
  .progress-indicator{
    height: $progress-indicator-height;
    background: $vue-green;
  }
}

.wrapper{
  max-width: (240px+40px+20px) * 4;
  overflow: hidden;
  margin: 0 auto;
  /*position: absolute;*/
  top: 20%;
  left: 5%;
}
.v-carousel{
  display: flex;
  transition: all ease 1s;
}
.left{
  background-image: url(../img/left.svg);
  width: 60px;
  height: 60px;
  background-position: center;
  border: 1px solid #C8D9FB;
  background-color: transparent;
  background-repeat: no-repeat;
  margin: 40px 20px;
}
.left:hover{
  background-color: #C8D9FB;
}
.right{
  background-image: url(../img/right.svg);
  width: 60px;
  height: 60px;
  background-position: center;
  border: 1px solid #C8D9FB;
  background-color: transparent;
  background-repeat: no-repeat;
  margin: 40px 20px;
}
.right:hover{
  background-color: #C8D9FB;
}
@media (max-width: 1110px){
  .wrapper{
  max-width: (240px+40px+20px) *3;
}
}
@media (max-width: 820px){
  .wrapper{
    max-width: (240px+40px+20px) *2;
  }
  .head{
    display: grid;
  }
  .progress-indicator-wrapper{
    margin-top: 30px;
    margin-left: 0%;
  }
}
@media (max-width: 542px){
  .wrapper{
    max-width: (240px+40px+20px) *1;
  }
}

</style>
