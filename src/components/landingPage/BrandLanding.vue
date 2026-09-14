<script>
import { RouterLink } from "vue-router";
import Back from "./assets/icons/back.vue";
import { useBrandsStore } from "../../stores/brands";
import { registerRuntimeCompiler } from "vue";
export default {
  setup() {
    const brandStore = useBrandsStore();

    return {
      brandStore,
    };
  },
  components: {
    Back,
  },
  computed: {
    brand() {
      return this.brandStore.brands[this.$route.params.brandName];
    },
    cssLinearGradient() {
      return `linear-gradient(180deg, rgba(255, 255, 255, 1) 0%, ${this.brand.cssGradient} 100%)`;
    },
    bgLetterColor() {
      return this.brand.bgLetterColor;
    },
    carName() {
      return this.brand.carName;
    },
    bgName() {
      return this.brand.bgName;
    },
    firstLink() {
      return this.brand.firstLink;
    },
    secondLink() {
      return this.brand.secondLink;
    },
    thirdLink() {
      return this.brand.thirdLink;
    },
  },
};
</script>

<template>
  <div class="container-wrapper">
    <span class="brand-name">{{ $route.params.brandName.toUpperCase() }}</span>
    <RouterLink to="/">
      <div class="return-home-page">
        <button>
          <Back />
          <span>Back</span>
        </button>
      </div>
    </RouterLink>
  </div>
  <section class="hero">
    <div class="hero-background">
      <span>{{ bgName }}</span>
      <div class="image-landing-page">
        <img :src="brand.landingImg" />
      </div>
    </div>
  </section>
  <div class="details">
    <div class="details-subtitle">
      <span class="span-link-subtitle">
        <a href="">{{ firstLink }}</a>
        <a href="">{{ secondLink }}</a>
        <a href="">{{ thirdLink }}</a>
      </span>
      <h1>{{ carName }}</h1>
      <label>Gasoline</label>
    </div>
    <div class="listing-items">
      <hr />
    </div>
  </div>
</template>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Serif:ital,opsz,wght@0,8..144,100..900;1,8..144,100..900&display=swap");
@font-face {
  font-family: "911Porscha";
  src: url("./assets/fonts/fontFormate/911porschav3.ttf") format("truetype");
  font-weight: normal;
  font-style: normal;
}
.container-wrapper {
  display: flex;
  justify-content: center;
  text-align: center;
  padding: 30px;
  border: 1px solid #c0c0c0;
  background-color: white;
  width: 100%;
  box-sizing: border-box;
  position: sticky;
  top: 0;
  z-index: 100000;
  /* padding-top: 116px; */
}
.brand-name {
  font-size: clamp(22px, 2vw, 32px);
  letter-spacing: clamp(2px, 0.3vw, 4px);
  font-family: "911Porscha", sans-serif;
}
.return-home-page {
  position: absolute;
  top: 22px;
  left: 30px;
  background-color: transparent;
}

.return-home-page button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4px;
  padding: 10px 20px 10px 10px;
  border: 1px solid gray;
  font-weight: 600;
  border-radius: 4px;
  color: #555;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 14px;
  background-color: white;
  cursor: pointer;
}

.hero {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 100%;
}
.hero-background {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: clamp(360px, 48vh, 600px);
  max-height: 600px;
  width: 100%;
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 1) 0%,
    rgb(214, 214, 214) 100%
  );
  background: v-bind(cssLinearGradient);
}
.hero-background span {
  position: absolute;
  z-index: 2;
  top: 20%;
  font-size: clamp(5.5rem, 16vw, 16rem);
  line-height: 0.85;
  max-width: 100%;
  overflow: hidden;
  font-family: "911Porscha", sans-serif;
  font-weight: bold;
  /* color: #c0c0c0; */
  color: v-bind(bgLetterColor);
  text-align: center;
}
.image-landing-page {
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  width: min(70%, 1200px);
  max-width: 1200px;
  top: 85%;
  z-index: 100;
  transform: translateY(-50%);
}
.image-landing-page > img {
  width: 100%;
  height: auto;
  object-fit: contain;
  max-width: none;
  transform: scale(1.3);
  max-height: none;
}
.details-subtitle {
  margin-top: clamp(100px, 8vw, 180px);
}
.details-subtitle {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.details-subtitle span {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 30px;
}
.details-subtitle h1 {
  font-size: clamp(2rem, 4vw, 3rem);
  font-family: "911Porscha", sans-serif;
  font-weight: bolder;
}
.span-link-subtitle a {
  /* text-decoration: none; */
  color: black;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: lighter;
  font-size: 18px;
}
.details-subtitle label {
  font-size: 14px;
  padding: 6px 20px 6px 20px;
  background-color: #e9e9e9;
  border-radius: 6px;
}
.listing-items {
  padding: 20px 136px 0px 136px;
}
hr {
  border-top: 1px solid #ccc;
}

@media (max-width: 1024px) {
  .listing-items {
    padding-left: 60px;
    padding-right: 60px;
  }

  .image-landing-page {
    width: min(76%, 900px);
  }
}

@media (max-width: 768px) {
  .container-wrapper {
    min-height: 68px;
    padding: 20px 88px;
  }

  .return-home-page {
    top: 14px;
    left: 16px;
  }

  .return-home-page button {
    min-height: 40px;
    padding: 8px 12px 8px 8px;
  }

  .hero-background {
    height: clamp(300px, 54vw, 430px);
  }

  .hero-background span {
    top: 18%;
    font-size: clamp(5rem, 22vw, 10.5rem);
  }

  .image-landing-page {
    width: 82%;
    top: 82%;
  }

  .image-landing-page > img {
    transform: scale(1.15);
  }

  .details-subtitle {
    margin-top: clamp(78px, 14vw, 116px);
    padding: 0 20px;
  }

  .details-subtitle span {
    flex-wrap: wrap;
    gap: 10px 22px;
  }

  .span-link-subtitle a {
    font-size: 16px;
  }

  .details-subtitle h1 {
    margin: 24px 0;
    text-align: center;
  }

  .listing-items {
    padding: 20px 20px 0;
  }
}

@media (max-width: 480px) {
  .container-wrapper {
    min-height: 60px;
    padding: 17px 72px;
  }

  .brand-name {
    font-size: 20px;
  }

  .return-home-page {
    top: 10px;
    left: 10px;
  }

  .return-home-page button {
    min-height: 38px;
    padding: 7px 10px 7px 6px;
    font-size: 13px;
  }

  .hero-background {
    height: 270px;
  }

  .hero-background span {
    top: 20%;
    font-size: clamp(4.2rem, 23vw, 6rem);
  }

  .image-landing-page {
    width: 92%;
    top: 82%;
  }

  .image-landing-page > img {
    transform: scale(1.08);
  }

  .details-subtitle {
    margin-top: 72px;
    padding: 0 16px;
  }

  .details-subtitle h1 {
    font-size: 1.8rem;
    margin: 20px 0;
  }

  .span-link-subtitle a {
    font-size: 14px;
  }

  .listing-items {
    padding: 16px 16px 0;
  }
}
</style>
