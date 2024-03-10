<script setup>
import { onMounted } from 'vue';
import { gsap } from "gsap";

import { CustomEase } from "gsap/CustomEase";
import { RoughEase, ExpoScaleEase, SlowMo } from "gsap/EasePack";

import { Flip } from "gsap/Flip";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { Observer } from "gsap/Observer";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";
import { Draggable } from "gsap/Draggable";
import { MotionPathPlugin } from "gsap/MotionPathPlugin";
import { EaselPlugin } from "gsap/EaselPlugin";
import { PixiPlugin } from "gsap/PixiPlugin";
import { TextPlugin } from "gsap/TextPlugin";

gsap.registerPlugin(Flip, ScrollTrigger, Observer, ScrollToPlugin, Draggable, MotionPathPlugin, EaselPlugin, PixiPlugin, TextPlugin, RoughEase, ExpoScaleEase, SlowMo, CustomEase);

function animateFrom(elem, direction) {
  direction = direction || 1;
  var x = 0,
    y = direction * 100;
  if (elem.classList.contains("gs_reveal_fromLeft")) {
    x = -100;
    y = 0;
  } else if (elem.classList.contains("gs_reveal_fromRight")) {
    x = 100;
    y = 0;
  }
  elem.style.transform = "translate(" + x + "px, " + y + "px)";
  elem.style.opacity = "0";
  gsap.fromTo(elem, { x: x, y: y, autoAlpha: 0 }, {
    duration: 1.25,
    x: 0,
    y: 0,
    autoAlpha: 1,
    ease: "expo",
    overwrite: "auto"
  });
}

function hide(elem) {
  gsap.set(elem, { autoAlpha: 0 });
}

onMounted(() => {

  gsap.from('#promotion', { y: -1000, ease: "power3.out", duration: 2 })

  gsap.to("[data-speed]", {
    y: (i, el) => (1 - parseFloat(el.getAttribute("data-speed"))) * ScrollTrigger.maxScroll(window),
    ease: "none",
    scrollTrigger: {
      start: 0,
      end: "max",
      invalidateOnRefresh: true,
      scrub: 0
    }
  });

  gsap.utils.toArray(".gs_reveal").forEach(function (elem) {
    hide(elem); // assure that the element is hidden when scrolled into view

    ScrollTrigger.create({
      trigger: elem,
      // markers: true,
      onEnter: function () { animateFrom(elem) },
      onEnterBack: function () { animateFrom(elem, -1) },
      onLeave: function () { hide(elem) } // assure that the element is hidden when scrolled into view
    });
  });

})

</script>

<template>

  <nav id="nav">
    <div class="title">
      <h1>PSUEDOCARDS</h1>
    </div>
    <div class="itch">
      <img src="/itch.svg" alt="">
    </div>
  </nav>
  <main class="crt">
    <div id="hero">
      <div class="">
        <h1 data-speed="0.75" class="title-main">PSUEDOCARDS</h1>
        <p data-speed="1.2">A card based game for algorithm simulation using Godot Engine</p>
      </div>

    </div>
    <div id="promotion" data-scroll-section>

      <div class="vid">
        <video autoplay="autoplay" playsinline loop="loop" width="100%" muted="muted">
          <source src="/autoplay.mp4" type="video/mp4">
        </video>
        <div class="text-center desc  " data-speed="1">
          <p data-speed="1.3">
            Test your algorithm-building skills in PsuedoCards! Connect the cards in order to solve specific
          problems.
          Levels will include limitations for you to work and think of your way in finishing the task.
        </p>
          
        </div>
      </div>





    </div>
  </main>


</template>

<style scoped>
@keyframes fadeEffect {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}

#nav {
  height: 70px;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100;
  /* border: 1px solid red; */
  padding: 10px;
  mix-blend-mode: difference;
  color: white;

  display: flex;
  justify-content: space-between;
  align-items: center;

  animation: fadeEffect 4s;
}

#nav .title h1 {
  font-family: TF;
  text-align: center;


}

#nav .itch img {
  width: 100%;
  height: 2rem;
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

#hero h1 {
  font-size: 124px;
  font-family: TF;
  animation: fadeEffect 2s;

}

#hero p {
  text-align: center;
  font-size: 24px;
  animation: fadeEffect 3s;

}

#promotion {
  background-color: black;
  height: 100%;
  width: 100%;

}

.desc {
  z-index: 2;
  color: white;
  font-size: 40px;
  position: absolute;
  top: 0;
  left: 0;

  height: 100%;

  background-color: rgba(0, 0, 0, 0.5);

  animation: fadeEffect 5s;

  display: flex;
  align-items: center;
  justify-content: center;

  line-height: 1.5;
}

.vid {
  width: 100%;
}

.vid video {
  max-height: 500px;
  width: 100%;
  display: inline-block;
  vertical-align: baseline;
  overflow: hidden;

  object-fit: cover;

}
</style>
