<template>
  <div class="wrapper" :class="{ dark: scrolled }" :style="{ background: bgColor }">
    <div class="container">
      <div class="menu-btn">
        <svg @click="$emit('toggle-sidebar')" class="burger-svg" xmlns="http://www.w3.org/2000/svg" width="2rem"
          height="2rem" viewBox="0 0 24 24" :fill="textColor">
          <path d="M3 4H21V6H3V4ZM3 11H21V13H3V11ZM3 18H21V20H3V18Z"></path>
        </svg>
        <p @click="$router.push('/')" class="goldman-regular">Carbodia</p>
      </div>
      <div class="search-wrapper">
        <div class="search">
          <svg class="search-icon" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor">
            <path
              d="M18.031 16.6168L22.3137 20.8995L20.8995 22.3137L16.6168 18.031C15.0769 19.263 13.124 20 11 20C6.032 20 2 15.968 2 11C2 6.032 6.032 2 11 2C15.968 2 20 6.032 20 11C20 13.124 19.263 15.0769 18.031 16.6168ZM16.0247 15.8748C17.2475 14.6146 18 12.8956 18 11C18 7.1325 14.8675 4 11 4C7.1325 4 4 7.1325 4 11C4 14.8675 7.1325 18 11 18C12.8956 18 14.6146 17.2475 15.8748 16.0247L16.0247 15.8748Z">
            </path>
          </svg>
          <input v-model="query" @input="$emit('search-cars', query)" type="text" class="search-bar"
            placeholder="Search"></input>
        </div>
      </div>
      <LoginButton :textColor="textColor" :borderColor="textColor === 'black' ? (scrolled ? 'rgba(0, 0, 0, 0.8)' : 'rgba(0, 0, 0, 0.6)') : (scrolled ? 'rgba(0, 0, 0, 0.8)' : 'rgba(255, 255, 255, 0.8)')" />
    </div>

    <div class="brand-navs">
      <RouterLink class="brand" to="/brand/ferrari">
        <div class="brand">
          <div>
            <FerrariNavIcon :color="textColor" :width="'20px'" :height="'24px'" />
          </div>
          <p class="quattrocento-bold">Ferrari</p>
        </div>
      </RouterLink>
      <RouterLink class="brand" to="/brand/mercedes">
        <div class="brand">
          <div>
            <MercedesNavIcon :color="textColor" :width="'20px'" :height="'24px'" />
          </div>
          <p class="quattrocento-bold">Mercedes</p>
        </div>
      </RouterLink>
      <RouterLink class="brand" to="/brand/porsche">
        <div class="brand">
          <div>
            <PorscheNavIcon :color="textColor" :width="'20px'" :height="'24px'" />
          </div>
          <p class="quattrocento-bold">Porsche</p>
        </div>
      </RouterLink>
      <RouterLink class="brand" to="brand/lamborghini">
        <div class="brand">
          <div>
            <LamboNavIcon :color="textColor" :width="'20px'" :height="'24px'" />
          </div>
          <p class="quattrocento-bold">Lamboghini</p>
        </div>
      </RouterLink>
      <RouterLink class="brand" to="brand/bmw">
        <div class="brand">
          <div>
            <BmwNavIcon :color="textColor" :width="'20px'" :height="'24px'" />
          </div>
          <p class="quattrocento-bold">BMW</p>
        </div>
      </RouterLink>
    </div>
  </div>
</template>

<script>
import BmwNavIcon from '@/components/icons/NavIcons/BmwNavIcon.vue';
import FerrariNavIcon from '@/components/icons/NavIcons/FerrariNavIcon.vue';
import LamboNavIcon from '@/components/icons/NavIcons/LamboNavIcon.vue';
import MercedesNavIcon from '@/components/icons/NavIcons/MercedesNavIcon.vue';
import PorscheNavIcon from '@/components/icons/NavIcons/PorscheNavIcon.vue';
import LoginButton from '@/components/navigation/LoginButton.vue';
export default {
  components: {
    FerrariNavIcon,
    MercedesNavIcon,
    PorscheNavIcon,
    BmwNavIcon,
    LamboNavIcon,
    LoginButton,
  },
  props: {
    textColor: {
      default: "transparent",
    },
    borderColor: {
      default: "#C0C0C0",
    },
    bgColor: {
      default: "rgba(255, 255, 255, 0.1)",
    },
    scrolled: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      query: '',
    }
  }
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Goldman:wght@400;700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Quicksand:wght@300..700&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Goldman:wght@400;700&family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Quattrocento+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Quattrocento:wght@400;700&family=Quicksand:wght@300..700&display=swap");

.wrapper {
  position: fixed;
  width: 100vw;
  z-index: 168;
  background: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.15);
  top: 0;
  left: 0;
  right: 0;
  transition: all 0.6s ease;
}

.dark {
  background: white !important;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2) !important;
}

.dark .search-icon {
  color: black;
}

.dark .brand-navs::-webkit-scrollbar-thumb {
  background: rgba(0, 0, 0, 0.3);
}

.container {
  display: flex;
  justify-content: space-around;
  align-items: center;
  height: 65px;
}

.search {
  position: relative;
  width: auto;
  overflow: visible;
}

.search-wrapper {
  position: relative;
  overflow: visible;
}

.search>input {
  padding-left: 2.5rem;
  box-sizing: border-box;
  width: 35vw;
}

.search-icon {
  position: absolute;
  width: 16px;
  top: 8px;
  left: 12px;
  color: grey;
  transition: color 0.6s ease;
}

.search-bar {
  font-family: "Rajdhani", sans-serif;
  height: 30px;
  width: 500px;
  border: none;
  border-radius: 20px;
  padding: 1rem;
  box-sizing: border-box;
  border: 1px solid;
  border-color: v-bind(borderColor);
  background-color: white;
  outline: none;
  transition: all 0.3s ease;
}

.search-bar:focus {
  outline: none;
  border-color: v-bind(borderColor);
}

.menu-btn {
  display: flex;
  position: relative;
  align-items: center;
  cursor: pointer;
  color: v-bind(textColor);
  transition: color 0.4s ease;
}

.menu-btn>p {
  font-size: 1.8rem;
  color: v-bind(textColor);
}

.burger-svg {
  position: absolute;
  left: -44px;
  transition: fill 0.6s ease;
}

.brand-navs {
  padding: 1.2rem 0 1.2rem 0;
  height: 12px;
  display: flex;
  justify-content: center;
  column-gap: 4rem;
  border: 1px solid;
  border-color: v-bind(borderColor);
  border-right: none;
  border-left: none;
  transition: border-color 0.6s ease;
}

.brand-navs .brand {
  display: flex;
  align-items: center;
  column-gap: 1rem;
  cursor: pointer;
  text-decoration: none;
}

.brand-navs svg {
  transition: fill 0.6s ease;
}

.brand>p {
  position: relative;
  font-size: 14px;
  bottom: 2px;
  color: v-bind(textColor);
}

.goldman-regular {
  font-family: "Goldman", sans-serif;
  font-weight: 400;
  font-style: normal;
  transition: color 0.4s ease;
}

.goldman-bold {
  font-family: "Goldman", sans-serif;
  font-weight: 700;
  font-style: normal;
}

.quattrocento-sans-regular {
  font-family: "Quattrocento Sans", sans-serif;
  font-weight: 400;
  font-style: normal;
}

.quattrocento-bold {
  font-family: "Rajdhani", sans-serif;
  font-weight: 700;
  font-style: normal;
  transition: color 0.4s ease;
}

/* Responsive Styles */

/* Tablets and smaller (max-width: 1024px) */
@media (max-width: 1024px) {
  .container {
    padding: 0 1.5rem;
    justify-content: space-between;
  }

  .search-wrapper {
    flex: 1;
    max-width: 45%;
    margin: 0 1rem;
  }

  .search>input {
    width: 100%;
  }

  .brand-navs {
    column-gap: 2rem;
  }

  .menu-btn>p {
    font-size: 1.5rem;
  }

  .burger-svg {
    left: -36px;
  }
}

/* Tablets portrait and smaller (max-width: 768px) */
@media (max-width: 768px) {
  .container {
    height: 55px;
    padding: 0 0.5rem;
  }

  .search>input {
    width: 30vw;
    font-size: 14px;
  }

  .search-icon {
    width: 14px;
    top: 7px;
  }

  .menu-btn>p {
    font-size: 1.3rem;
  }

  .burger-svg {
    left: -32px;
    width: 1.5rem;
    height: 1.5rem;
  }

  .brand-navs {
    column-gap: 1.5rem;
    padding: 1rem 0.5rem;
    overflow-x: auto;
    justify-content: flex-start;
    -webkit-overflow-scrolling: touch;
  }

  .brand-navs::-webkit-scrollbar {
    height: 4px;
  }

  .brand-navs::-webkit-scrollbar-track {
    background: transparent;
  }

  .brand-navs::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.3);
    border-radius: 2px;
  }
}

/* Mobile devices (max-width: 480px) */
@media (max-width: 480px) {
  .wrapper {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border-bottom: 1px solid rgba(255, 255, 255, 0.15);
  }

  .container {
    display: grid;
    grid-template-columns: auto minmax(0, 1fr) auto;
    column-gap: 8px;
    height: 60px;
    padding: 0 0.75rem;
    background: inherit;
  }

  .menu-btn {
    grid-column: 1;
    flex-shrink: 0;
    min-width: 0;
  }

  .menu-btn>p {
    font-size: 1.1rem;
  }

  .burger-svg {
    position: static;
    width: 1.4rem;
    height: 1.4rem;
  }

  .search-wrapper {
    grid-column: 2;
    width: 100%;
    max-width: none;
    min-width: 0;
    margin: 0;
    overflow: visible;
  }

  .search {
    width: 100%;
    min-width: 0;
    overflow: visible;
  }

  .search>input {
    width: 100%;
    min-width: 0;
    font-size: 13px;
    padding: 0.6rem 0.6rem 0.6rem 2.2rem;
    height: 36px;
    background-color: white;
    border-radius: 18px;
  }

  .container > :last-child {
    grid-column: 3;
    min-width: 36px;
  }

  .search-icon {
    width: 14px;
    top: 11px;
    left: 10px;
  }

  /* Brand navigation - horizontal scroll */
  .brand-navs {
    display: flex;
    column-gap: 1.5rem;
    padding: 1rem 1rem;
    overflow-x: auto;
    overflow-y: hidden;
    justify-content: flex-start;
    white-space: nowrap;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: thin;
    background: inherit;
  }

  .brand-navs::-webkit-scrollbar {
    height: 3px;
  }

  .brand-navs::-webkit-scrollbar-track {
    background: rgba(255, 255, 255, 0.1);
  }

  .brand-navs::-webkit-scrollbar-thumb {
    background: rgba(255, 255, 255, 0.3);
    border-radius: 3px;
  }

  .brand-navs .brand {
    column-gap: 0.6rem;
    flex-shrink: 0;
    padding: 0.25rem;
  }

  .brand>p {
    font-size: 12px;
    white-space: nowrap;
  }

  .brand svg {
    width: 18px !important;
    height: 22px !important;
  }
}

/* Extra small devices (max-width: 360px) */
@media (max-width: 360px) {
  .container {
    padding: 0 0.75rem;
    height: 56px;
  }

  .menu-btn>p {
    display: none;
  }

  .burger-svg {
    position: static;
    width: 1.3rem;
    height: 1.3rem;
  }

  .search-wrapper {
    margin: 0;
  }

  .search>input {
    font-size: 12px;
    height: 34px;
    padding: 0.5rem 0.5rem 0.5rem 2rem;
  }

  .search-icon {
    width: 13px;
    top: 10px;
    left: 9px;
  }

  .brand-navs {
    column-gap: 1.25rem;
    padding: 0.75rem 0.75rem;
  }

  .brand>p {
    font-size: 11px;
  }

  .brand svg {
    width: 16px !important;
    height: 20px !important;
  }
}
</style>
