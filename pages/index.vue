<template>
  <div>
    <div data-relative-input="true" id="scene">
      <div data-depth="0.9" class="bg-cloud-wrapp">
        <img  :style="'transform: translateY('+bgVars.offsetY+'%) translateX(-50%);filter: brightness(' +(bgVars.filter - 0.3) +');'" class="bg-cloud" src="img/wave-haikei.svg" alt="">

      </div>
      <div data-depth="0.7" class="bg-cloud-wrapp">

        <img  :style="'transform:  translateY('+(bgVars.offsetY +1)+'%) translateX(-'+(bgVars.offsetX +15)+'%);filter: brightness(' +(bgVars.filter - 0.2) +');'" class="bg-cloud" src="img/wave-haikei.svg" alt="">
      </div>
      <div data-depth="0.5" class="bg-cloud-wrapp">

        <img  :style="'transform:  translateY('+(bgVars.offsetY +3)+'%) translateX(-'+(bgVars.offsetX +20)+'%);filter: brightness(' +(bgVars.filter - 0.1) +');'" class="bg-cloud" src="img/wave-haikei.svg" alt="">
      </div>

    </div>
  </div>

</template>


<style>
#scene {
  position: relative !important;
  background-color: #21D4FD;
  background-image: linear-gradient(19deg, #17b6ff 38%, #3d7ee9 100%);



  height: 100vh;
  overflow: hidden !important;

}
.bg-cloud {
  position: absolute !important;
  bottom: 0;
  left: 50%;
  width: 200%;
}

.bg-cloud-wrapp {
  position: absolute !important;
  height: 100%;
  width: 100%;
  left: 0;
  bottom: 0;
}
</style>
<script>
import Parallax from 'parallax-js'
import navbar from "@/components/navbar";
export default {
  name : "index",
  components:{
    navbar
  },
  data() {
    return {
      bgVars : {
        offsetY : 30,
        offsetX : 50,
        filter : 1
      }
    }
  },
  mounted() {
    let scene = document.getElementById('scene');
    let parallaxInstance = new Parallax(scene);
  }
}
</script>
