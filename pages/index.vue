<template>
  <div>
    <div data-relative-input="true" id="scene">
      <div data-depth="0.9" class="bg-cloud-wrapp">
        <img
          :style="
            'transform: translateY(' +
              bgVars.offsetY +
              '%) translateX(-50%);filter: brightness(' +
              (bgVars.filter - 0.2) +
              ');'
          "
          class="bg-cloud"
          src="img/wave1.svg"
          alt=""
        />
      </div>
      <div data-depth="0.7" class="bg-cloud-wrapp">
        <img
          :style="
            'transform:  translateY(' +
              (bgVars.offsetY + 1) +
              '%) translateX(-' +
              (bgVars.offsetX + 15) +
              '%);filter: brightness(' +
              (bgVars.filter - 0.2) +
              ');'
          "
          class="bg-cloud"
          src="img/wave1.svg"
          alt=""
        />
      </div>
      <div data-depth="0.5" class="bg-cloud-wrapp">
        <img
          :style="
            'transform:  translateY(' +
              (bgVars.offsetY + 5) +
              '%) translateX(-30%);filter: brightness(' +
              (bgVars.filter - 0.1) +
              ');'
          "
          class="bg-cloud"
          src="img/wave1.svg"
          alt=""
        />
      </div>
      <div data-depth="0.4" class="bg-cloud-wrapp">
        <img
          :style="
            'transform:  translateY(' +
              (bgVars.offsetY + 5) +
              '%) translateX(-' +
              (bgVars.offsetX + 15) +
              '%);filter: brightness(' +
              (bgVars.filter - 0.2) +
              ');'
          "
          class="bg-cloud"
          src="img/wave1.svg"
          alt=""
        />
      </div>
    </div>
    <div class="search-container ">
      <div class="search-inputs d-flex">
        <div class="input-control">
        <b-form-input
          class="search-input"
          v-model="searchInput.fromInput"
          placeholder="Из"
        ></b-form-input></div>
        <div class="input-control"><b-form-input
          class="search-input"
          v-model="searchInput.toInput"
          placeholder="Куда"
        ></b-form-input></div>
        <div class="input-control"><b-form-datepicker
          class="search-input"
          v-model="searchInput.dateTo"
          placeholder="Туда"
        ></b-form-datepicker></div>
        <div class="input-control"><b-form-datepicker
          class="search-input"
          v-model="searchInput.dateBack"
          placeholder="Обратно"
        ></b-form-datepicker></div>
      </div>
      <div class="p-05">
        <b-button block variant="info" class="glass-button" >
        ПОИСК
        </b-button>
      </div>
    </div>
  </div>
</template>

<style>
#scene {
  position: relative !important;
  background-color: #21d4fd;
  background-image: linear-gradient(19deg, #17b6ff 38%, #3d7ee9 100%);

  min-height: 100vh;
  overflow: hidden !important;
}
.bg-cloud {
  position: absolute !important;
  bottom: 0;
  left: 50%;
  width: 200%;
  opacity: 0.5;
}
.d-flex {
  display: flex;
  justify-content: space-between;
  
}
.m-05 {
  margin: 0.5em;  

}
.p-05 {
  padding: 0.5em;  

}
.search-container {
  position: absolute;
  padding: 2em;
  left: 50%;
  bottom : 20%;
  transform: translateX(-50%);
  background: rgba(255, 255, 255, 0.35);

  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.18);

}
.glass-button {
   display: block;
   padding:7px 14px;
   border: 0;
   text-decoration: none;
   border-radius: 15px;
   background-color: rgba(255, 255, 255, 0.034);
   border: 1px solid rgba(255, 255, 255, 0.219);
   backdrop-filter: blur(30px);
   color: rgba(255, 255, 255, 0.904);
   font-size: 14px;
   letter-spacing: 2px;
   font-weight: bold;
   cursor: pointer;
   text-transform: uppercase;
 }
.search-input {
  
  display: block;
}
.input-control {
  padding: 0.5em;  
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
import Parallax from "parallax-js";
import navbar from "@/components/navbar";
export default {
  name: "index",
  components: {
    navbar
  },
  data() {
    return {
      bgVars: {
        offsetY: 10,
        offsetX: 50,
        filter: 1.3
      },
      searchInput: {
        fromInput: "",
        toInput: "",
        dateTo: "",
        dateBack: "",
        passenger: ""
      }
    };
  },
  mounted() {
    let scene = document.getElementById("scene");
    let parallaxInstance = new Parallax(scene);
  }
};
</script>
