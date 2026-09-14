<template>
  <div class="bg">
    <transition :name="bgTransition" mode="in-out">
      <img :key="currBg" :src="currBg" alt="" />
    </transition>
    <div class="title-wrapper">
      <h4 class="title caudex-bold">{{ currentTitle }}</h4>
      <p class="subtitle">
        {{ currentSubtitle }}
      </p>
    </div>

    <div class="indicator-container">
      <div class="center-container">
        <div class="indicator-wrapper">
          <template v-for="n in bgUrls.length">
            <transition name="fade">
              <div
                class="indicator"
                :class="{ 'indicator-active': bgIndex === n - 1 }"
              ></div>
            </transition>
          </template>

          <div class="skip-icon">
            <svg
              @click="btnPrevImg"
              class="arrow-btn prev"
              width="24"
              height="16"
              viewBox="0 0 20 12"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M4.78554 5.24992H20V6.74992H4.78554L11.4905 10.7729L9.72275 11.8335L0 5.99992L9.72275 0.16626L11.4905 1.22692L4.78554 5.24992Z"
                fill="white"
                fill-opacity="0.8"
              />
            </svg>
            <svg
              @click="btnNextImg"
              class="arrow-btn arrow-right next"
              width="24"
              height="16"
              viewBox="0 0 20 12"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M4.78554 5.24992H20V6.74992H4.78554L11.4905 10.7729L9.72275 11.8335L0 5.99992L9.72275 0.16626L11.4905 1.22692L4.78554 5.24992Z"
                fill="white"
                fill-opacity="0.8"
              />
            </svg>
          </div>
        </div>
        <span>{{ currentTagline }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";
import { Transition } from "vue";
import car1 from "@/assets/images/landing-bgs/car1.jpeg";
import car2 from "@/assets/images/landing-bgs/car2.png";
import car3 from "@/assets/images/landing-bgs/car3.png";
import car4 from "@/assets/images/landing-bgs/car4.png";
import car5 from "@/assets/images/landing-bgs/car5.png";

export default {
  data() {
    return {
      bgUrls: [car1, car2, car3, car4, car5],
      firstLoad: true,
      bgIndex: 0,
      bgTransition: "slide-fade-right",
      bgTransitionInterval: () => setInterval,
    };
  },

  methods: {
    nextImg() {
      if (this.bgIndex == this.bgUrls.length - 1) {
        this.bgIndex = 0;
      } else {
        this.bgIndex = this.bgIndex + 1;
      }
      this.bgTransition = "slide-fade-right";
    },
    prevImage() {
      if (this.bgIndex == 0) {
        this.bgIndex = this.bgUrls.length - 1;
      } else {
        this.bgIndex = this.bgIndex - 1;
      }
      this.bgTransition = "slide-fade-left";
    },
    btnNextImg() {
      this.nextImg();
      this.refreshTransitionInterval();
    },
    btnPrevImg() {
      this.prevImage();
      this.refreshTransitionInterval();
    },
    refreshTransitionInterval() {
      clearInterval(this.bgTransitionInterval);
      this.bgTransitionInterval = setInterval(this.nextImg, 5000);
    },
  },
  computed: {
    currBg() {
      return this.bgUrls[this.bgIndex];
    },
    currentTitle() {
      const titles = [
        "Porsche 911 GT3 RS",
        "Ferrari SF90 Stradale",
        "Mercedes-Benz G-Wagon",
        "Lamborghini Huracan",
        "BMW M8 Competition",
      ];
      return titles[this.bgIndex] || "Luxury Car";
    },
    currentSubtitle() {
      const subtitles = [
        "Dominate the track with the Porsche 911 GT3 RS. A racing-bred supercar that brings professional-grade performance to the streets with 525 horsepower and precision handling.",
        "Hybrid hypercar excellence with the Ferrari SF90 Stradale. Combining a twin-turbo V8 with electric motors for 986 horsepower and breathtaking acceleration from 0-60 in 2.5 seconds.",
        "Conquer any terrain with the legendary Mercedes-Benz G-Wagon. The ultimate off-road luxury SUV that combines rugged capability with sophisticated comfort and prestige.",
        "Unleash fury with the Lamborghini Huracan. A mid-engine supercar delivering 602 horsepower through its naturally aspirated V10, offering pure Lamborghini performance and style.",
        "Experience the pinnacle of BMW performance with the M8 Competition. A grand tourer that blends 617 horsepower with luxurious comfort for the ultimate driving experience.",
      ];
      return (
        subtitles[this.bgIndex] ||
        "Discover the pinnacle of automotive excellence with our curated collection of the world's most prestigious luxury vehicles. From Italian supercars to German engineering mastery."
      );
    },
    currentTagline() {
      const taglines = [
        "Track-Ready Performance",
        "Hybrid Supercar Revolution",
        "Unstoppable Luxury",
        "V10 Fury Unleashed",
        "M Performance Mastery",
      ];
      return taglines[this.bgIndex] || "Experience automotive luxury redefined";
    },
  },
  mounted() {
    this.bgTransitionInterval = setInterval(this.nextImg, 5000);
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Caudex:ital,wght@0,400;0,700;1,400;1,700&family=Goldman:wght@400;700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Quattrocento+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Quattrocento:wght@400;700&family=Quicksand:wght@300..700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Roboto+Flex:opsz,wght@8..144,100..1000&family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap");

.bg {
  position: relative;
  height: 100svh;
  width: 100vw;
  background-size: 100% auto;
  padding: 0;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.bg > img {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -200;
  object-fit: cover;
  object-position: center;
}

.center-container {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  color: white;
  font-family: "Roboto Flex", sans-serif;
  font-style: italic;
  font-weight: lighter;
}

.title-wrapper {
  position: absolute;
  display: flex;
  flex-direction: column;
  width: min(46vw, 600px);
  left: clamp(32px, 8vw, 120px);
  bottom: clamp(48px, 8vh, 80px);
}

.title {
  color: white;
  font-size: clamp(34px, 3.5vw, 48px);
  margin: 0;
  line-height: 1.1;
}

.subtitle {
  color: white;
  font-style: italic;
  font-family: "Rajdhani", sans-serif;
  font-weight: 300;
  font-size: clamp(13px, 1vw, 14px);
  line-height: 1.45;
}

.indicator-container {
  display: flex;
  flex-direction: column;
  position: absolute;
  bottom: clamp(56px, 9vh, 92px);
  right: clamp(32px, 8vw, 120px);
}

.indicator-container > div {
  margin: 0;
  padding: 0;
}

.indicator-wrapper {
  display: flex;
  align-items: center;
  column-gap: 8px;
  padding-bottom: 14px;
}

.skip-icon {
  display: flex;
  align-items: center;
  padding-left: 20px;
}

.indicator {
  width: 36px;
  height: 2px;
  background-color: rgb(206, 206, 206);
}

.indicator-active {
  width: 36px;
  height: 4px;
  background-color: white;
  transition: background-color 1s ease;
}

.arrow-btn {
  cursor: pointer;
  padding-right: 5px;
}

.arrow-right {
  transform: rotate(180deg);
}

.caudex-regular {
  font-family: "Rajdhani", sans-serif;
  font-weight: 400;
  font-style: normal;
}

.caudex-bold {
  font-family: "Rajdhani", sans-serif;
  font-weight: 700;
  font-style: normal;
  font-size: 50px;
}

.fade-enter-from {
  opacity: 0;
}

.fade-enter-to {
  opacity: 1;
}

.fade-leave-from {
  opacity: 1;
}

.fade-leave-to {
  opacity: 0;
}

.fade-enter-active {
  transition: opacity 0.5s;
}

.fade-leave-active {
  transition: opacity 0.5s;
}

.slide-fade-right-enter-from {
  opacity: 0;
  transform: translateX(100%);
}

.slide-fade-right-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-fade-right-leave-from {
  transform: translateX(0);
}

.slide-fade-right-leave-to {
  transform: translateX(-100%);
}

.slide-fade-right-enter-active {
  transition: all 0.5s;
}

.slide-fade-right-leave-active {
  transition: all 0.5s;
}

.slide-fade-left-enter-from {
  opacity: 0;
  transform: translateX(-100%);
}

.slide-fade-left-enter-to {
  opacity: 1;
  transform: translateX(0);
}

.slide-fade-left-leave-from {
  transform: translateX(0);
}

.slide-fade-left-leave-to {
  transform: translateX(100%);
}

.slide-fade-left-enter-active {
  transition: transform 0.5s;
}

.slide-fade-left-leave-active {
  transition: transform 0.5s;
}

/* Responsive Styles */

/* Tablets and smaller (max-width: 1024px) */
@media (max-width: 1024px) {
  .title-wrapper {
    width: 400px;
    left: 80px;
    bottom: 100px;
  }

  .title {
    font-size: 38px;
    line-height: 1.1;
  }

  .subtitle {
    font-size: 13px;
  }

  .indicator-container {
    right: 80px;
    bottom: 120px;
  }

  .caudex-bold {
    font-size: 38px;
  }
}

/* Tablets portrait and smaller (max-width: 768px) */
@media (max-width: 768px) {
  .bg {
    height: 100vh;
  }

  .bg > img {
    object-fit: cover;
    min-height: 100%;
    min-width: 100%;
    object-position: center;
  }

  .title-wrapper {
    width: 400px;
    left: 50px;
    bottom: 140px;
  }

  .title {
    font-size: 36px;
    line-height: 1.2;
    margin-bottom: 15px;
  }

  .subtitle {
    font-size: 13px;
    line-height: 1.5;
  }

  .indicator-container {
    right: 50px;
    bottom: 90px;
  }

  .indicator-wrapper {
    column-gap: 8px;
    padding-bottom: 12px;
  }

  .indicator {
    width: 30px;
  }

  .indicator-active {
    width: 35px;
  }

  .arrow-btn {
    width: 20px;
    height: 16px;
  }

  .center-container > span {
    font-size: 13px;
    text-align: center;
    padding: 0 15px;
  }

  .caudex-bold {
    font-size: 36px;
  }
}

/* Mobile devices (max-width: 480px) */
@media (max-width: 480px) {
  .bg {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    margin-top: 0;
    padding-top: 0;
  }

  .bg > img {
    object-fit: cover;
    min-height: 100%;
    width: 100%;
    object-position: center;
    top: 0;
  }

  .title-wrapper {
    width: auto;
    left: 16px;
    right: 16px;
    bottom: 150px;
    z-index: 2;
  }

  .title {
    font-size: 28px;
    line-height: 1.2;
    margin-bottom: 12px;
  }

  .subtitle {
    font-size: 12px;
    line-height: 1.5;
    max-width: none;
  }

  .indicator-container {
    position: absolute;
    right: 50%;
    transform: translateX(50%);
    bottom: 80px;
    width: 100%;
    z-index: 2;
  }

  .center-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
  }

  .indicator-wrapper {
    column-gap: 6px;
    padding-bottom: 12px;
    justify-content: center;
  }

  .indicator {
    width: 24px;
    height: 2.5px;
  }

  .indicator-active {
    width: 30px;
    height: 3px;
  }

  .skip-icon {
    padding-left: 15px;
  }

  .arrow-btn {
    width: 18px;
    height: 14px;
    padding-right: 4px;
  }

  .center-container > span {
    font-size: 11px;
    max-width: 85%;
    text-align: center;
    line-height: 1.4;
  }

  .caudex-bold {
    font-size: 28px;
  }
}

/* Extra small devices (max-width: 360px) */
@media (max-width: 360px) {
  .bg {
    height: 100vh;
  }

  .bg > img {
    object-fit: cover;
    min-height: 100%;
    width: 100%;
  }

  .title-wrapper {
    left: 12px;
    right: 12px;
    bottom: 140px;
  }

  .title {
    font-size: 28px;
    line-height: 1.1;
    margin-bottom: 10px;
  }

  .subtitle {
    font-size: 11px;
    line-height: 1.4;
  }

  .indicator-container {
    bottom: 75px;
  }

  .indicator-wrapper {
    column-gap: 5px;
    padding-bottom: 10px;
  }

  .indicator {
    width: 20px;
    height: 2px;
  }

  .indicator-active {
    width: 26px;
    height: 2.5px;
  }

  .arrow-btn {
    width: 16px;
    height: 12px;
  }

  .center-container > span {
    font-size: 10px;
    max-width: 80%;
  }

  .caudex-bold {
    font-size: 28px;
  }
}
</style>
