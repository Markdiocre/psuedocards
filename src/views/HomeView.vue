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

function goToItch() {
  window.location.assign('https://markdiocre.itch.io/psuedocards')
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
    <div class="itch" @click="goToItch()">
      <img src="/itch.svg" alt="">
    </div>

  </nav>
  <main>
    <div id="hero">
      <div class="crt">
        <h1 data-speed="0.75" class="title-main">PSUEDOCARDS</h1>
        <p data-speed="1.2">A card based game for algorithm simulation using Godot Engine</p>
      </div>
    </div>
    <div id="promotion" data-scroll-section>

      <div class="vid">
        <video autoplay="autoplay" playsinline loop="loop" width="100%" muted="muted">
          <source src="/autoplay.mp4" type="video/mp4">
        </video>
        <div class="text-center desc" data-speed="1">
          <p>
            Test your algorithm-building skills in PsuedoCards!
          </p>

        </div>
      </div>
    </div>

    <div id="hows">
      <div class="container">
        <div class="col-lg-12">
          <div class="row">
            <h2 class="text-center h2">CHECK THE PSUEDO-CARDS</h2>
          </div>
          <div class="row">
            <div class="col-md-4 mt-3">
              <div class="hows-panel">
                <h4>INPUT</h4>
                <p>Accept an input and make it the current value</p>
              </div>
            </div>
            <div class="col-md-4 mt-3">
              <div class="hows-panel">
                <h4>OUTPUT</h4>
                <p>Send the current value to output</p>
              </div>
            </div>
            <div class="col-md-4 mt-3">
              <div class="hows-panel">
                <h4>ARITHMETIC</h4>
                <p>Perform Addition, Subtraction, Multiplication, Divison, or Modulo to a certain index value</p>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-md-3 mt-3">
            <div class="hows-panel">
              <h4>JUMP
              </h4>
              <p>Used to go to a card with previous connections</p>
            </div>
          </div>
          <div class="col-md-3 mt-3">
            <div class="hows-panel">
              <h4>JUMP IF</h4>
              <p>If conditions are met, the flow will go through THEN, if not then it will go through ELSE</p>
            </div>
          </div>
          <div class="col-md-3 mt-3">
            <div class="hows-panel">
              <h4>STORE</h4>
              <p>Store current value to an index value</p>
            </div>
          </div>
          <div class="col-md-3 mt-3">
            <div class="hows-panel">
              <h4>COPY</h4>
              <p>Copy from an index value and make it the current value</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div id="screenshot">
      <div class="container">
        <div class="col-lg-12">
          <div class="row p-2">
            <h2 class="text-center">HERE ARE SOME INGAME SCREENSHOTS!</h2>
          </div>
          <div class="row">
            <div id="carouselExampleIndicators" class="carousel slide">
              <div class="carousel-indicators">
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active"
                  aria-current="true" aria-label="Slide 1"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1"
                  aria-label="Slide 2"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2"
                  aria-label="Slide 3"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="3"
                  aria-label="Slide 4"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="4"
                  aria-label="Slide 5"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="5"
                  aria-label="Slide 6"></button>
                <button type="button" data-bs-target="#carouselExampleIndicators" data-bs-slide-to="6"
                  aria-label="Slide 7"></button>
              </div>
              <div class="carousel-inner">
                <div class="carousel-item active">
                  <img src="/1.png" class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                  <img src="/2.png" class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                  <img src="/3.png" class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                  <img src="/4.png" class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                  <img src="/5.png" class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                  <img src="/6.png" class="d-block w-100" alt="...">
                </div>
                <div class="carousel-item">
                  <img src="/7.png" class="d-block w-100" alt="...">
                </div>
              </div>
              <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleIndicators"
                data-bs-slide="prev">
                <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Previous</span>
              </button>
              <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleIndicators"
                data-bs-slide="next">
                <span class="carousel-control-next-icon" aria-hidden="true"></span>
                <span class="visually-hidden">Next</span>
              </button>
            </div>
          </div>
        </div>
      </div>

    </div>

    <div id="itch" @click="goToItch()">
      <h1 class="text-center">AVAILABLE ON ITCH.IO</h1>
    </div>

    <div id="footer">
      <div class="container">
        <div class="row">
          <div class="col-lg-4">
            <div class="d-flex justify-content-center align-items-center">
              <div>
                <h4>DEVELOPED BY:</h4>
                <p>MARK THADDEUS R. MANUEL</p>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="d-flex justify-content-center align-items-center">
              <div>
                <div><img src="/vvl.png" height="70px"></div>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="d-flex">
              <a class="icon" href="https://www.facebook.com/PsuedoCards"><svg xmlns="http://www.w3.org/2000/svg" width="32"
                  height="32" fill="currentColor" class="bi bi-facebook" viewBox="0 0 16 16">
                  <path
                    d="M16 8.049c0-4.446-3.582-8.05-8-8.05C3.58 0-.002 3.603-.002 8.05c0 4.017 2.926 7.347 6.75 7.951v-5.625h-2.03V8.05H6.75V6.275c0-2.017 1.195-3.131 3.022-3.131.876 0 1.791.157 1.791.157v1.98h-1.009c-.993 0-1.303.621-1.303 1.258v1.51h2.218l-.354 2.326H9.25V16c3.824-.604 6.75-3.934 6.75-7.951" />
                </svg></a>

                <div @click="goToItch()" class="ps-2" style="cursor: pointer;"> <img src="/app-icon.svg" alt="" width="32px"></div >
            </div>
          </div>
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
  height: 500px;
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
  width: 100%;

  background-color: rgba(0, 0, 0, 0.5);

  animation: fadeEffect 5s;

  display: flex;
  align-items: center;
  justify-content: center;

  line-height: 1.5;
}

.vid {
  width: 100%;
  height: 100%;
}

.vid video {
  max-height: 100%;
  width: 100%;
  display: inline-block;
  vertical-align: baseline;
  overflow: hidden;

  object-fit: cover;

}

#about {
  height: 100vh;
}

.panel {
  height: 100vh;
}

#hows {
  height: 100%;
  color: white;
  background-color: #1e1e1e;
  padding-top: 20px;
  padding-bottom: 20px;
}

.hows-panel {
  border: #96ce00 1px solid;
  height: 100%;
  padding: 10px;
}

.hows-panel:hover {
  background-color: #96ce00;
  color: #1e1e1e;
  transform: scale(1.1);
  transition: 0.2s ease;
  cursor: pointer;

}

p {
  margin: 0px;
}

#screenshot {
  color: white;
  background-color: #1e1e1e;
  padding: 20px;
}

#itch {
  background-color: #FF244A;
}

#itch h1 {
  margin: 0px;
}

#itch:hover {
  color: white;
  background-color: #96ce00;
  cursor: pointer;
}

#footer {
  padding: 20px;
  text-decoration: none;
}

#footer .icon svg{
  height: 32px;
}
</style>
