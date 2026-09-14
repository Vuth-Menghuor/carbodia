<template>
  <div class="container">
    <div class="layout-sec">
      <div class="column">
        <div class="header-col">
          <span>{{ name }}</span>
          <input class="star" type="checkbox" title="bookmark page" checked />
        </div>
        <div class="sport">Sport</div>
        <div ref="carImage" class="popular-car">
          <img :src="img" loading="lazy" alt="car1" />
        </div>
        <div class="bg-popular"></div>
        <div class="details">
          <span>
            <gas />
            <span class="space-txt">90L</span>
          </span>
          <span>
            <GroupPeople />
            <span class="space-txt">2 People</span>
          </span>
          <span>
            <speedo />
            <span class="space-txt">211 mph</span>
          </span>
        </div>
        <div class="price-inquire">
          <button class="btn-price">{{ price }}</button>
          <button class="btn-buy">Inquire</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import speedo from "@/components/icons/popIcons/speedo.vue";
import gas from "@/components/icons/popIcons/gas.vue";
import GroupPeople from "@/components/icons/popIcons/groupPeople.vue";
import gsap from "gsap";

export default {
  props: {
    name: "",
    img: "",
    price: 0,
    themeColor: "red",
    imgHeight: "160px",
    isVisible: Boolean,
  },
  data() {
    return {
      color: this.themeColor || "gray",
      height: this.imgHeight || "160px",
    };
  },
  components: {
    gas,
    GroupPeople,
    speedo,
  },
  methods: {
    revealCar() {
      gsap.to(this.$refs.carImage, {
        duration: 1.1,
        xPercent: -50,
        ease: "power2.out",
      });
    },
  },
  mounted() {
    gsap.set(this.$refs.carImage, { xPercent: 50 });
    if (this.isVisible) this.revealCar(); 
  },
  watch: {
    isVisible(visible) {
      if (visible) this.revealCar();
    },
  },
  computed: {
    linearGradient() {
      return `linear-gradient(90deg, #ffffff 18%, ${this.color} 100%)`;
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Goldman:wght@400;700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Quattrocento+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Raleway:ital,wght@0,100..900;1,100..900&family=Roboto+Flex:opsz,wght@8..144,100..1000&family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Goldman:wght@400;700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Noto+Sans:ital,wght@0,100..900;1,100..900&family=Quattrocento+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Rajdhani:wght@300;400;500;600;700&family=Raleway:ital,wght@0,100..900;1,100..900&family=Roboto+Flex:opsz,wght@8..144,100..1000&family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap");
.container h1 {
  font-size: 38px;
  font-family: "Raleway", sans-serif;
  font-optical-sizing: auto;
  font-weight: bold;
}
.container {
  width: 100%;
  min-width: 0;
}
.layout-sec {
  display: flex;
  justify-content: space-between;
  width: 100%;
  min-width: 0;
}
.column {
  overflow: hidden;
  border: 2px solid #bababa;
  height: 380px;
  width: 100%;
  min-width: 0;
  box-sizing: border-box;
  border-radius: 10px;
  position: relative;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}
.column .header-col {
  display: flex;
  justify-content: space-between;
  padding: 30px 0px 0px 30px;
  align-items: center;
  font-family: "Raleway", sans-serif;
  font-size: 18px;
  font-weight: 600;
}
.star {
  visibility: hidden;
  font-size: 36px;
  bottom: 20px;
  right: 42px;
  position: relative;
  cursor: pointer;
}
.star::after {
  content: "\2605";
  visibility: visible;
  color: black;
}
.star:checked::after {
  color: #a8a8a8;
  content: "\2606";
}
.sport {
  color: #b8b8b8;
  font-size: 18px;
  font-family: "Raleway", sans-serif;
  font-weight: 600;
  padding: 14px 0px 0px 30px;
}
.popular-car {
  position: absolute;
  left: 50%;
  bottom: 135px;
  transform: translateX(0%);
}

.popular-car img {
  height: v-bind(height);
  width: auto;
  transform: scale(1.2);
}

.bg-popular {
  position: relative;
  height: 180px;
  width: 800px;
  top: 120px;
  background: v-bind(linearGradient);
  box-shadow: 0px 6px 5px rgb(190, 190, 190);
  rotate: -22.83deg;
  z-index: -100;
}

.bg-popular-ferrari {
  position: relative;
  height: 180px;
  width: 620px;
  right: 50px;
  top: 100px;
  background: rgb(255, 255, 255);
  background: linear-gradient(
    90deg,
    rgba(255, 255, 255, 1) 18%,
    rgba(255, 0, 0, 1) 100%
  );
  rotate: -22.83deg;
  z-index: -100;
}
.bg-popular-car3 {
  position: relative;
  height: 180px;
  width: 620px;
  right: 50px;
  top: 100px;
  background: #ffffff;
  background: linear-gradient(90deg, #ffffff 18%, #0066ff 100%);
  rotate: -22.83deg;
  z-index: -100;
}
.details {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  align-items: center;
  padding: 10px 30px 0px 30px;
}

.details span {
  display: flex;
  align-items: center;
  min-width: 0;
  white-space: nowrap;
}

.details > span:nth-child(2) {
  justify-content: center;
}

.details > span:last-child {
  justify-content: flex-end;
}

.space-txt {
  padding: 0px 0px 0px 6px;
  font-family: "Rajdhani", sans-serif;
  font-weight: 400;
  font-size: clamp(14px, 1.5vw, 20px);
  font-style: normal;
}
.price-inquire {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 20px;
  padding: 20px 30px 0px 30px;
}
.btn-price {
  border: none;
  border-radius: 8px;
  width: 100%;
  min-width: 0;
  box-sizing: border-box;
  font-family: "Rajdhani", sans-serif;
  background: rgb(255, 255, 255);
  font-size: 20px;
  font-weight: 500;
  /* background: linear-gradient(90deg, rgba(255,255,255,1) 0%, rgba(165,165,165,1) 100%);     */
  background: v-bind(linearGradient);
  padding: 10px 20px 10px 20px;
  cursor: pointer;
}

.btn-buy {
  padding: 10px 20px 10px 20px;
  width: 100%;
  min-width: 0;
  box-sizing: border-box;
  border: none;
  color: white;
  background-color: v-bind("themeColor");
  font-family: "Raleway", sans-serif;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
}

/* Responsive adjustments */
@media (max-width: 2250px) {
  .popular-car img {
    transform: scale(1.1);
  }
}

@media (max-width: 1200px) {
  .popular-car img {
    transform: scale(1);
  }
}

@media (max-width: 992px) {
  .popular-car img {
    transform: scale(0.9);
  }
  .column {
    height: 360px;
  }
}

@media (max-width: 768px) {
  .popular-car img {
    transform: scale(0.8);
  }
  .column {
    height: 340px;
  }
}

@media (max-width: 576px) {
  .popular-car img {
    transform: scale(0.65);
  }

  .column {
    height: 370px;
  }

  .column .header-col {
    padding: 20px 16px 0;
    font-size: 16px;
  }

  .header-col > span {
    min-width: 0;
    overflow-wrap: anywhere;
  }

  .star {
    right: 20px;
    bottom: 16px;
  }

  .sport {
    padding: 10px 16px 0;
    font-size: 15px;
  }

  .popular-car {
    bottom: 138px;
  }

  .details {
    padding: 8px 16px 0;
  }

  .space-txt {
    padding-left: 4px;
    font-size: 14px;
  }

  .details svg {
    width: 15px;
    height: 15px;
  }

  .price-inquire {
    gap: 10px;
    padding: 16px 16px 0;
  }

  .btn-price,
  .btn-buy {
    padding: 10px 8px;
    font-size: 15px;
  }
}
</style>
