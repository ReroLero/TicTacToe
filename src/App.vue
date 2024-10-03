<script setup>
import Game from './game/Game.vue'
</script>

<template>
  <div class="page">
    <video class="vid" autoplay loop muted>
      <source src="./assets/vd.mp4" type="video/webm" />
      <source src="./assets/vd.mp4" type="video/mp4" />
    </video>
   <div class="mainBlock">
    <Game />
    </div>
  </div>
 
</template>

<style scoped>

.page {
  position: relative;
  height: 100dvh;
  width: 100dvw;
  display: flex;
  justify-content: center;
  align-items: center;
}

.vid {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

backg{
  display: flex;
  flex-direction: row;
  position: absolute;
  align-items: center;  
  padding: 0;
  width: 1920px;
  height: 1080px;
}

.mainBlock {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0%;
  top: 0%;
  background: cover;
  background-size: cover;
  background-repeat: no-repeat;

  display: flex;
  align-items: center;  
  padding: 0;
}

</style>
