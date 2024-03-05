<template>
  <main data-scroll-container class="crt">
    <div id="hero" data-scroll-section>
      <div>
        <h1 data-scroll data-scroll-speed="1">PSUEDOCARDS</h1>
        <p data-scroll data-scroll-speed="3">A card based game for algorithm simulation using Godot Engine</p>
      </div>
      
    </div>
    <div id="promotion" data-scroll-section>
      <h2 data-scroll data-scroll-speed="1">What's up?</h2>
      <p data-scroll data-scroll-speed="2">😬</p>
    </div>
  </main>


</template>

<style scoped>

@keyframes flicker {
  0% {
  opacity: 0.27861;
  }
  5% {
  opacity: 0.34769;
  }
  10% {
  opacity: 0.23604;
  }
  15% {
  opacity: 0.90626;
  }
  20% {
  opacity: 0.18128;
  }
  25% {
  opacity: 0.83891;
  }
  30% {
  opacity: 0.65583;
  }
  35% {
  opacity: 0.67807;
  }
  40% {
  opacity: 0.26559;
  }
  45% {
  opacity: 0.84693;
  }
  50% {
  opacity: 0.96019;
  }
  55% {
  opacity: 0.08594;
  }
  60% {
  opacity: 0.20313;
  }
  65% {
  opacity: 0.71988;
  }
  70% {
  opacity: 0.53455;
  }
  75% {
  opacity: 0.37288;
  }
  80% {
  opacity: 0.71428;
  }
  85% {
  opacity: 0.70419;
  }
  90% {
  opacity: 0.7003;
  }
  95% {
  opacity: 0.36108;
  }
  100% {
  opacity: 0.24387;
  }
}

.crt::after {
  content: " ";
  display: block;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%), linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
  z-index: 0;
  background-size: 100% 2px, 3px 100%;
  pointer-events: none;
}

#hero {
  height: 100vh;
  

  color: black;

  display: flex;
  justify-content: center;
  align-items: center;

  z-index: 2;

  padding: 20px;
}

#hero h1{
  font-size: 124px;
  font-family: TF;
}

#hero p{
  text-align: center;
  font-size: 24px;
}

#promotion {
  height: 60vh;
  background-color: rgba(0, 255, 255, 0.149);
}
</style>

<script setup>
import { onMounted } from 'vue';
import LocomotiveScroll from "locomotive-scroll";



onMounted(()=>{
  const scroll = new LocomotiveScroll({
    el: document.querySelector('[data-scroll-container]'),
    smooth: true
});
})

</script>