<script>
import { mapState } from "pinia";
import FooterComponent from "../FooterComponent.vue";
import Back from "./Back.vue";
import { useCarStore } from "../../stores/cars";
export default {
  components: {
    Back,
    FooterComponent,
  },
  computed: {
    ...mapState(useCarStore, {
      cars: "cars",
      imageUrls(store) {
        const urls = [];
        const id = this.$route.params.carId;
        const car = store.getCar(id);
        car.images.forEach((img) => {
          urls.push(store.getImageURL("cars", id, img));
        });
        console.log(car.images);

        return urls;
      },
    }),
  },
};
</script>

<template>
  <Back />
  <div class="container">
    <div class="grid-container">
      <div class="grid-header">
        <img
          v-for="img in imageUrls.slice(0, 2)"
          :src="img"
          class="header-image"
        />
      </div>
      <div class="grid-main">
        <img
          v-for="img in imageUrls.slice(2, 5)"
          :src="img"
          class="main-image"
        />
        <!-- <img src="@/assets/images/products/car4.png" class="main-image" />
        <img src="@/assets/images/products/car5.png" class="main-image" /> -->
      </div>
      <div class="grid-footer">
        <img
          v-for="img in imageUrls.slice(5, 7)"
          :src="img"
          class="footer-image"
        />

        <!-- <img src="@/assets/images/products/car4.png" class="footer-image" /> -->
      </div>
      <div class="last-gallery">
        <img :src="imageUrls[imageUrls.length - 1]" />
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Container Styling */
.container {
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #ffffff;
  box-sizing: border-box;
}

/* Grid Container Styling */
.grid-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
  width: 100%;
  max-width: 1800px;
  background-color: #ffffff; /* White background for a clean look */
  border-radius: 10px; /* Rounded corners */
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 10px; /* Subtle shadow */
  padding: 20px; /* Internal spacing */
  margin-top: 50px;
  box-sizing: border-box;
}

/* Header Section */
.grid-header {
  display: flex;
  justify-content: space-between;
  gap: 10px;
}

.grid-header img {
  width: calc(50% - 5px);
  height: auto;
  object-fit: cover;
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
/* 
.grid-header img:hover {
  transform: scale(1.05);
  box-shadow: rgba(0, 0, 0, 0.2) 0px 6px 12px;
} */

/* Main Section */
.grid-main {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.grid-main img {
  height: auto;
  width: 33%;
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
/* 
.grid-main img:hover {
  transform: scale(1.05);
  box-shadow: rgba(0, 0, 0, 0.2) 0px 6px 12px;
} */

/* Footer Section */
.grid-footer {
  display: flex;
  justify-content: space-between;
  gap: 10px;
}

.grid-footer img {
  width: calc(50% - 5px);
  height: auto;
  object-fit: cover;
  border-radius: 5px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
/* 
.grid-footer img:hover {
  transform: scale(1.05);
  box-shadow: rgba(0, 0, 0, 0.2) 0px 6px 12px;
} */

/* Last Gallery Section */
.last-gallery {
  display: flex;
  justify-content: center;
  width: 100%;
}

.last-gallery > img {
  width: 100%;
  object-fit: cover;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px;
  cursor: pointer;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

/* .last-gallery > img:hover {
  transform: scale(1.05);
  box-shadow: rgba(0, 0, 0, 0.2) 0px 6px 12px;
} */

@media (max-width: 768px) {
  .container {
    padding: 16px;
  }

  .grid-container {
    margin-top: 24px;
    padding: 12px;
    gap: 12px;
  }

  .grid-header,
  .grid-main,
  .grid-footer {
    gap: 8px;
  }
}

@media (max-width: 480px) {
  .container {
    padding: 10px;
  }

  .grid-container {
    margin-top: 16px;
    padding: 8px;
    gap: 8px;
  }

  .grid-header,
  .grid-main,
  .grid-footer {
    flex-direction: column;
    gap: 8px;
  }

  .grid-header img,
  .grid-main img,
  .grid-footer img {
    width: 100%;
  }
}
</style>
