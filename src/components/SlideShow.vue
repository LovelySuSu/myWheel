<template>
  <div class="slide-show" @mouseover="clearTimer" @mouseout="runInterval">
    <div class="slide-img">
        <transition name="slide" v-if="isShow">
          <img :src="slideList[nowIndex].src">
        </transition>
    </div>
    <div class="slide-page">
      <p class="page-index" @click="goPage(preIndex)">&lt;</p>
      <p v-for="(item,index) in slideList" :class="{ 'current': index == nowIndex}" class="page-index" @click="goPage(index)">{{index+1}}</p>
      <p class="page-index" @click="goPage(nextIndex)">&gt;</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'slide',
  props:['slideList','speed'],
  data () {
    return {
      nowIndex:0,
      isShow:true
    }
  },
  computed:{
    preIndex(){
      if (this.nowIndex === 0) {
        return this.slideList.length - 1
      }
      else {
        return this.nowIndex - 1
      }
    },
    nextIndex(){
      if (this.nowIndex === this.slideList.length - 1) {
        return 0
      }
      else {
        return this.nowIndex + 1
      }
    },
  },
  methods:{
    goPage(index){
        this.isShow = false;
        setTimeout(() => {this.nowIndex = index;this.isShow=true}, 10);
    },
    runInterval(){
      this.timer = setInterval(() => {this.goPage(this.nextIndex)}, this.speed);
    },
    clearTimer(){
      clearInterval(this.timer);
    }
  },
  mounted(){
   this.runInterval();
  }
}
</script>


<style scoped>
  .slide-enter-active, .slide-leave-active {
    transition: all .5s;
  }
  .slide-enter, .slide-leave-to {
    transform: translateX(-500px);
  }
  .slide-show {
    position: relative;
    margin: 15px 15px 15px 0;
    width: 500px;
    height: 300px;
    overflow: hidden;
  }
  .slide-img {
    width: 100%;
  }
  .slide-img img {
    width: 100%;
    position: absolute;
    top: 0;
    background-position: center;
  }
  .slide-page{
    display: flex;
    background: rgba(233,233,233,0.8);
    position:absolute;
    bottom: 0;
    height: 30px;
    width: 100%;
  }
  .slide-page .page-index{
    line-height: 15px;
    font-size: 16px;
    margin: 10px;
    color: plum;
    cursor: pointer;
  }
  .slide-page .current{
    color:palevioletred;
  }
</style>
